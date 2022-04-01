<template>
  <div id="app">
    <AppLayout>
      <div class="main-grid">
        <div class="left-block">
          <ProductForm @submitForm="formSubmit"/>
        </div>
        <div class="right-block">
          <ProductFilter @filterChange="handleFilter" />
          <div v-if="isProductsFetched">
            <transition-group class="product-card-grid" name="card" mode="out-in" tag="div">
              <div class="product-card-grid__item" v-for="(item, index) in allProducts" :key="item.id">
                <ProductCard
                  @delete="deleteItem" 
                  :key="index" 
                  :id="item.id" 
                  :name="item.name" 
                  :desc="item.desc" 
                  :link="item.link" 
                  :price="item.price"/>
              </div>  
            </transition-group>
          </div>
          <Spinner v-else />
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
import Spinner from './components/Spinner.vue'

export default {
  name: 'App',
  components: {
    AppLayout,
    ProductForm,
    ProductFilter,
    ProductCard,
    Toast,
    Spinner
  },
  data() {
    return {
      allProducts: [{
        id: 1648816193658,
        name: "Наименование товара",
        desc: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
        price: "10000",
        link: "https://cdn.shopify.com/s/files/1/0441/1349/4174/products/1_polaroid_camera_1280x.jpg?v=1611942552"
      }],
      showSuccess: false,
      isProductsFetched: false,
    }
  },
  mounted() {
    const products = JSON.parse(window.localStorage.getItem('products'));
    if(!products) {
      window.localStorage.setItem('products', JSON.stringify(this.allProducts))
    }
    else {
      this.allProducts = products;
    }
    this.isProductsFetched = true;
  },
  methods: {
    formSubmit(form) {
      this.allProducts.push(form);
      this.showSuccess = true;
      setTimeout(() => {
        this.showSuccess = false
      }, 2000)
      window.localStorage.setItem('products', JSON.stringify(this.allProducts))
    },
    deleteItem(id) {
      this.allProducts = this.allProducts.filter(item => item.id !== id);
      window.localStorage.setItem('products', JSON.stringify(this.allProducts))
    },
    handleFilter(value) {
      if(value === 'min') {
        this.allProducts.sort((a, b) => {
          return parseInt(a.price) - parseInt(b.price)
        })
      }
      if(value === 'max') {
        this.allProducts.sort((a, b) => {
          return  parseInt(b.price) - parseInt(a.price)
        })
      }
      if(value === 'name') {
        this.allProducts.sort((a, b) => {
          return a.name < b.name ? -1 : 1;
        })
      }
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

.card-enter-active, .card-leave-active {
  transition: all 0.4s;
}
.card-enter, .card-leave-to {
  opacity: 0;
  transition: 0.3s;
  // float: right;
  transform: translateY(100px);
}
.card-move {
  transition: transform 1s;
}
</style>
