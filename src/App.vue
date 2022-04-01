<template>
  <div id="app">
    <AppLayout>
      <div class="main-grid">
        <div class="left-block">
          <ProductForm />
        </div>
        <div class="right-block">
          <ProductFilter />
          <div class="product-card-grid">
          <template v-for="i in 10">
            <div class="product-card-grid__item" :key="i">
              <ProductCard />
            </div>
          </template>
          </div>
        </div>
      </div>
    </AppLayout>
  </div>
</template>

<script>
import AppLayout from './layouts/AppLayout'
import ProductForm from './components/ProductForm.vue'
import ProductFilter from './components/ProductFilter.vue'
import ProductCard from './components/ProductCard.vue'

export default {
  name: 'App',
  components: {
    AppLayout,
    ProductForm,
    ProductFilter,
    ProductCard
  }
}
</script>

<style lang="scss">
.main-grid {
  display: flex;
  gap: 16px;
}
.left-block {
  flex: 0 1 35%;
}
.right-block {
  flex: 0 1 75%;
}
.product-card-grid {
  margin-top: 16px;
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
  justify-content: space-between;
  align-items: stretch;
  &__item {
    flex: 0 0 calc(33% - 16px);
  }
}

@media only screen and (max-width: 1200px) {
  .product-card-grid {
    gap: 8px;
    &__item {
      flex: 0 0 calc(50% - 8px);
    }
  }
}

@media only screen and (max-width: 960px) {
  .main-grid {
    flex-wrap: wrap;
  }
  .left-block {
    flex: 0 0 100%;
  }
  .right-block {
    flex: 0 0 100%;
  }
  .product-card-grid {
    &__item {
      flex: 0 0 calc(33% - 8px);
    }
  }
}

@media only screen and (max-width: 640px) {
  .product-card-grid {
    &__item {
      flex: 0 0 calc(50% - 8px);
    }
  }
}

@media only screen and (max-width: 480px) {
  .product-card-grid {
    &__item {
      flex: 0 0 100%;
    }
  }
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
