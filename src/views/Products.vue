<template>
    <div>
      <ProductForm @product-added="addProduct" @product-edited="editProduct" />
      <ProductList 
        v-if="filteredProducts.length > 0" 
        :products="filteredProducts" 
        @delete-product="deleteProduct"
        @edit-product="setProductForEdit"
      />
      <p v-else>No products available. Please add a product.</p>
    </div>
  </template>
  
  <script>
  import ProductForm from '../components/ProductForm.vue';
  import ProductList from '../components/ProductList.vue';
  
  export default {
    components: {
      ProductForm,
      ProductList
    },
    data() {
      return {
        products: this.loadProducts(),
        productToEdit: null
      };
    },
    computed: {
      filteredProducts() {
        // Filter out null or invalid products
        return this.products.filter(product => product && typeof product === 'object');
      }
    },
    methods: {
      addProduct(newProduct) {
        this.products.push(newProduct);
        this.saveProducts();
      },
      editProduct(updatedProduct) {
        const index = this.products.findIndex(product => product.id === updatedProduct.id);
        if (index !== -1) {
          this.products.splice(index, 1, updatedProduct);
          this.saveProducts();
        }
      },
      deleteProduct(productId) {
        // Ensure productId is valid
        if (!productId) return; // Do nothing if productId is falsy
        this.products = this.products.filter(product => product.id !== productId);
        this.saveProducts();
      },
      setProductForEdit(product) {
        this.productToEdit = product;
      },
      saveProducts() {
        localStorage.setItem('products', JSON.stringify(this.products));
      },
      loadProducts() {
        const products = localStorage.getItem('products');
        return products ? JSON.parse(products) : [];
      }
    }
  };
  </script>
  
  <style scoped>
  /* Add your styles here */
  </style>
  