<template>
  <div class="product-table">
    <header class="main-header">
      <div class="logo">
        <Logo></Logo>
        <span>STORM</span>
      </div>

      <button class="hamburger" @click="toggleMobileMenu">
        <HamburgerIcon> </HamburgerIcon>
      </button>
      <div class="search">
        <SearchBar v-model="searchQuery" />
      </div>
      <div class="options">
        <button>
          <GearIcon></GearIcon>
        </button>
        <button>
          <NotificationsIcon></NotificationsIcon>
        </button>
        <button class="profile">
          <AvatarIcon></AvatarIcon>
          <span> Adriana Arias </span>
        </button>
      </div>

      <div class="mobile-menu" :data-open="mobileMenuOpen">
        <div class="options options-mobile">
          <button class="close" @click="toggleMobileMenu"><CloseIcon /></button>
          <button><GearIcon /> <span>Settings</span></button>
          <button><NotificationsIcon /> <span>Notifications</span></button>
          <button>
            <AvatarIcon />
            <span> Adriana Arias </span>
          </button>
        </div>
      </div>
    </header>
    <p class="results">
      <span>Products </span>
      <small>
        {{ filteredProducts.length }} of {{ products.length }} results.</small
      >
    </p>
    <table>
      <thead>
        <tr>
          <th class="id">ID</th>
          <th class="status" @click="sortBy('status')">Status</th>
          <th class="quantity" @click="sortBy('quantity')">Quantity</th>
          <th class="product" @click="sortBy('product')">Product Name</th>
          <th class="prices" @click="sortBy('total')">
            Prices <ChevronDownIcon />
          </th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="product in filteredProducts"
          :key="product.id"
          @click="openModal(product)"
        >
          <td class="id">{{ product.id }}</td>

          <td class="status">
            <span
              :class="
                productStatus(product.quantity)
                  .toLowerCase()
                  .replaceAll(' ', '-')
              "
            >
              {{ productStatus(product.quantity) }}
            </span>
          </td>
          <td class="quantity">{{ product.quantity }}</td>
          <td class="product">
            {{ product.product }} <br />
            <small>{{ product.serial }} </small> {{ ' ' }}
            <small class="qty-mobile"> - Qty: {{ product.quantity }} </small>
          </td>
          <td class="prices">${{ product.total | currency }}</td>
        </tr>
      </tbody>
    </table>
    <ProductModal
      v-if="selectedProduct"
      :product="selectedProduct"
      @close="selectedProduct = null"
    />
  </div>
</template>

<script setup>
import { computed, ref } from 'vue'

import AvatarIcon from '@/assets/icons/AvatarIcon.vue'
import ChevronDownIcon from '@/assets/icons/ChevronDownIcon.vue'
import GearIcon from '@/assets/icons/GearIcon.vue'
import Logo from '@/assets/icons/Logo.vue'
import NotificationsIcon from '@/assets/icons/NotificationsIcon.vue'
import productsData from '../data/products.json'
import ProductModal from './ProductModal.vue'
import SearchBar from './SearchBar.vue'
import HamburgerIcon from '@/assets/icons/HamburgerIcon.vue'
import CloseIcon from '@/assets/icons/CloseIcon.vue'

const searchQuery = ref('')
const selectedProduct = ref(null)
const sortKey = ref('product')
const sortOrder = ref(1)
const products = ref(productsData)
const mobileMenuOpen = ref(false)

const toggleMobileMenu = () => {
  mobileMenuOpen.value = !mobileMenuOpen.value
}

const openModal = (product) => {
  selectedProduct.value = product
}

const productStatus = (quantity) =>
  quantity > 50 ? 'In Stock' : quantity > 0 ? 'Low stock' : 'Out of stock'

const sortBy = (key) => {
  sortOrder.value = sortKey.value === key ? -sortOrder.value : 1
  sortKey.value = key
}

const filteredProducts = computed(() => {
  const query = searchQuery.value.toLowerCase()
  return products.value
    .filter((p) => p.product.toLowerCase().includes(query))
    .sort((a, b) =>
      a[sortKey.value] > b[sortKey.value] ? sortOrder.value : -sortOrder.value
    )
})
</script>

<style scoped lang="scss">
@use '../assets/scss/product-table.scss';
</style>
