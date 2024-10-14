<template>
  <form @submit.prevent="handleSubmit">
    <input v-model="product.name" placeholder="Product Name" required />
    <button type="submit">{{ isEdit ? 'Update Product' : 'Add Product' }}</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      product: {
        id: null,
        name: ''
      },
      isEdit: false
    };
  },
  props: {
    productToEdit: {
      type: Object,
      default: null
    }
  },
  watch: {
    productToEdit: {
      immediate: true,
      handler(newVal) {
        if (newVal) {
          this.product = { ...newVal }; // Set the form to the product being edited
          this.isEdit = true; // Set edit mode
        } else {
          this.resetForm();
        }
      }
    }
  },
  methods: {
    handleSubmit() {
      if (this.isEdit) {
        this.$emit('product-edited', this.product); // Emit the edited product
      } else {
        this.product.id = Date.now(); // Generate a unique ID
        this.$emit('product-added', this.product); // Emit the new product
      }
      this.resetForm();
    },
    resetForm() {
      this.product = { id: null, name: '' }; // Reset the product object
      this.isEdit = false; // Reset edit mode
    }
  }
};
</script>

<style scoped>
/* Add your styles here */
</style>
