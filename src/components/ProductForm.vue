<template>
  <form @submit.prevent="onSubmit" class="product-form">
    <input v-model="title" placeholder="Название товара" required />
    <textarea v-model="description" placeholder="Описание товара" required></textarea>
    <input type="number" v-model="price" placeholder="Цена" required />
    <button type="submit">Добавить товар</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      title: '',
      description: '',
      price: ''
    };
  },
  methods: {
    onSubmit() {
      const newProduct = {
        title: this.title,
        description: this.description,
        price: this.price,
        image: 'https://via.placeholder.com/150' 
      };
      this.$emit('add', newProduct);
      this.title = '';
      this.description = '';
      this.price = '';
    }
  }
};
</script>

<style scoped>
.product-form {
  background-color: #f0f3fa;
  padding: 20px;
  margin-top: 20px;
  border: 1px solid #ccc;
}

.product-form input,
.product-form textarea {
  width: 100%;
  margin-bottom: 10px;
  padding: 10px;
  font-size: 14px;
}

.product-form button {
  padding: 10px 20px;
  background-color: #787eff;
  color: #fff;
  border: none;
  cursor: pointer;
}

.product-form button:hover {
  background-color: #5555ff;
}
</style>