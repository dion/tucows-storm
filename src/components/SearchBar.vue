<template>
  <form action="" class="search-bar">
    <div class="search-input">
      <SearchIcon></SearchIcon>
      <input type="text" v-model="search" placeholder="Search..." />
    </div>
    <button class="search-button" type="submit">Search</button>
  </form>
</template>

<script setup>
import SearchIcon from '@/assets/icons/SearchIcon.vue'
import { ref, watch } from 'vue'
const props = defineProps(['modelValue'])
const emit = defineEmits(['update:modelValue'])

const search = ref(props.modelValue)
watch(search, (val) => emit('update:modelValue', val))
</script>

<style lang="scss">
@use '../assets/scss/global.scss';
@use '../assets/scss/_variables.scss';

.search-bar {
  display: flex;
  justify-content: space-between;
  gap: 16px;

  .search-input {
    flex-grow: 1;
    border-radius: 4px;
    border: 1px solid rgb(222, 222, 222);
    padding: 8px 16px;
    padding: 12px 20px;
    display: flex;
    align-items: center;
    gap: 8px;
    input {
      border: none;
      outline: none;
      width: 100%;
      &::placeholder {
        color: #bbb;
      }
    }
  }

  .search-button {
    background-color: variables.$color-accent;
    cursor: pointer;
    font-size: 0.9rem;
    padding: 12px 20px;
    color: white;
    border-radius: 4px;
    border: none;

    &:hover,
    &:active {
      background-color: #5548d9;
    }
  }
}
</style>
