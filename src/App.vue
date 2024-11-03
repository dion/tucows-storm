<template>
  <header>
    <nav>
      <!-- Navigation menu to transition to a hamburger menu on mobile -->
    </nav>
  </header>
  <main>
    <ProductTable />
  </main>
</template>

<script setup>
import ProductTable from './components/ProductTable.vue';
</script>

<style lang="scss">

// Media query for responsive mobile menu
@media (max-width: 768px) {
  nav {
    // Styles for mobile menu
  }
  h1 { 
    // color: $color-primary;
  }
}
</style>
