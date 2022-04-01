<template>
  <div id="app">
    <AppLayout>
      <div class="main-grid">
        <div class="left-block">
          <ProductForm @submitForm="formSubmit"/>
        </div>
        <div class="right-block">
          <ProductFilter />
          <transition-group class="product-card-grid" name="card" mode="out-in" tag="div">
            <div class="product-card-grid__item" v-for="(item, index) in allProducts" :key="index">
              <ProductCard :key="index" :name="item.name" :desc="item.desc" :link="item.link" :price="item.price"/>
            </div>  
          </transition-group>
        </div>
      </div>
      <Toast :isShown="this.showSuccess" />
    </AppLayout>
  </div>
</template>

<script>
import AppLayout from './layouts/AppLayout'
import ProductForm from './components/ProductForm.vue'
import ProductFilter from './components/ProductFilter.vue'
import ProductCard from './components/ProductCard.vue'
import Toast from './components/Toast.vue'

export default {
  name: 'App',
  components: {
    AppLayout,
    ProductForm,
    ProductFilter,
    ProductCard,
    Toast
  },
  data() {
    return {
      allProducts: [{
        name: "Наименование товара",
        desc: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
        price: "10000",
        link: "https://cdn.shopify.com/s/files/1/0441/1349/4174/products/1_polaroid_camera_1280x.jpg?v=1611942552"
      }],
      showSuccess: false,
    }
  },
  methods: {
    formSubmit(form) {
      this.allProducts.push(form);
      this.showSuccess = true;
      setTimeout(() => {
        this.showSuccess = false
      }, 2000)
      console.log('allproducts', this.allProducts);
    }
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
  // justify-content: space-between;
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

.card-enter-active, .list-leave-active {
  transition: all 1s;
}
.card-enter, .list-leave-to {
  opacity: 0.4;
  float: right;
  transform: translateX(100%);
}
</style>
