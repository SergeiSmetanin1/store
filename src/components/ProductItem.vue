<template>
  <div class="product-item">
    <h3>{{ product.title }}</h3>
    <img :src="product.image" alt="product image" />
    <p>{{ product.description }}</p>
    <p>{{ product.price }} $</p>
    <div class="buttons">
      <button @click="onEdit">Изменить</button>
      <button @click="onDelete">Удалить</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ['product'],
  methods: {
    onDelete() {
      this.$emit('delete', this.product.id);
    },
    onEdit() {
      this.$emit('edit', this.product);
    }
  }
};
</script>

<style scoped>
.product-item {
  background-color: #f9f9f9;
  border: 1px solid #ddd;
  padding: 15px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.product-item img {
  max-width: 100%;
  height: auto;
  margin-bottom: 10px;
}

.buttons {
  text-align: right;
}

.buttons button {
  margin-left: 10px;
  padding: 8px 15px;
  background-color: #787eff;
  color: #fff;
  border: none;
  cursor: pointer;
}

.buttons button:hover {
  background-color: #5555ff;
}
</style>