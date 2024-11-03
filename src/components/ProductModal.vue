<template>
  <div class="modal" @click.self="close">
    <article class="modal-card">
      <header>
        <h2>{{ product.product }}</h2>
        <button @click="close" class="close-x">
          <CloseIcon></CloseIcon>
        </button>
      </header>

      <div class="content">
        <img
          class="image"
          :src="product.image || placeholderImage"
          alt="Product Image"
        />

        <div class="info">
          <p><strong>Serial: </strong> {{ product.serial }}</p>
          <p>
            <strong>Description: </strong> Sample description of the product.
          </p>
          <p><strong>Price: </strong>${{ product.total | currency }}</p>
        </div>
      </div>

      <div class="close-btn">
        <button @click="close">Close</button>
      </div>
    </article>
  </div>
</template>

<script setup>
import CloseIcon from '@/assets/icons/CloseIcon.vue'
import { ref } from 'vue'
const props = defineProps({ product: Object })
const emit = defineEmits(['close'])
const placeholderImage = '/noimage.jpg'

const close = () => {
  emit('close')
}
</script>

<style scoped lang="scss">
.modal {
  position: fixed;
  z-index: 10;
  inset: 0;
  background-color: rgba(0, 0, 0, 0.2);
  backdrop-filter: blur(1px);

  display: grid;
  place-content: center;
  padding-inline: calc((100% - 800px) / 2);
}

.modal-card {
  background-color: white;
  box-shadow: 0 1px 6px rgba(0, 0, 0, 0.1);
  border-radius: 12px;
  padding: 32px;

  header {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    // align-items: center;
    margin-bottom: 32px;
    .close-x {
      background-color: transparent;
      border: none;
      cursor: pointer;
      padding: 0;
    }
  }

  .content {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 32px;
    .image {
      // aspect-ratio: 1/1;
      width: 100%;
      height: auto;
    }
    .info {
      text-wrap: balance;
    }
  }

  .close-btn {
    margin-top: 32px;
    display: flex;
    justify-content: flex-end;

    button {
      cursor: pointer;
      background-color: #eee;
      border: none;
      padding: 12px 20px;
      border-radius: 4px;
    }
  }
}

@media (width < 768px) {
  .modal-card {
    .content {
      grid-template-columns: 1fr;
    }
    .close-btn {
      flex-direction: column;
    }
  }
}
</style>
