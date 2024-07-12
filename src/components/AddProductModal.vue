<template>
  <div class="modal">
    <div class="modal-content">
      <span class="close" @click="onClose">&times;</span>
      <h2>Добавить новый товар</h2>
      <ProductForm @add="addProduct" />
    </div>
  </div>
</template>

<script>
import ProductForm from './ProductForm.vue';

export default {
  components: { ProductForm },
  methods: {
    onClose() {
      this.$emit('close');
    },
    addProduct(product) {
      this.$emit('add', product);
    }
  }
};
</script>

<style scoped>
.modal {
  display: block;
  position: fixed;
  z-index: 1;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  background-color: rgba(0, 0, 0, 0.4);
}

.modal-content {
  background-color: #fefefe;
  margin: 15% auto;
  padding: 20px;
  border: 1px solid #888;
  width: 80%;
  max-width: 500px;
}

.close {
  color: #aaa;
  float: right;
  font-size: 28px;
  font-weight: bold;
}

.close:hover,
.close:focus {
  color: black;
  text-decoration: none;
  cursor: pointer;
}
</style>