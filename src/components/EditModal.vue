<template>
  <div class="modal">
    <div class="modal-content">
      <span class="close" @click="onClose">&times;</span>
      <h2>Редактировать товар</h2>
      <form @submit.prevent="onSubmit">
        <input v-model="title" placeholder="Название товара" required />
        <textarea v-model="description" placeholder="Описание товара" required></textarea>
        <input type="number" v-model="price" placeholder="Цена" required />
        <button type="submit">Сохранить</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  props: ['product'],
  data() {
    return {
      title: this.product.title,
      description: this.product.description,
      price: this.product.price
    };
  },
  methods: {
    onClose() {
      this.$emit('close');
    },
    onSubmit() {
      const updatedProduct = {
        ...this.product,
        title: this.title,
        description: this.description,
        price: this.price
      };
      this.$emit('save', updatedProduct);
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
  color: #000;
  text-decoration: none;
  cursor: pointer;
}

.modal input,
.modal textarea {
  width: 100%;
  margin-bottom: 10px;
  padding: 10px;
  font-size: 14px;
  border: 1px solid #ccc;
}
</style>
