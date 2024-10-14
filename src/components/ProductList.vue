<template>
    <div>
      <ul>
        <li v-for="(product, index) in products" :key="product.id">
          {{ product.name }} <!-- Assuming each product has a 'name' property -->
          <button @click="editProduct(product)">Edit</button>
          <button @click="deleteProduct(product.id)">Delete</button>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      products: {
        type: Array,
        required: true
      }
    },
    methods: {
      editProduct(product) {
        this.$emit('edit-product', product);
      },
      deleteProduct(productId) {
        // Emit the productId for deletion
        this.$emit('delete-product', productId);
      }
    }
  };
  </script>
  
  <style scoped>
  /* Add your styles here */
  </style>
  