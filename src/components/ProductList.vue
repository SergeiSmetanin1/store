<template>
  <div class="main-section bg-grey">
    <h2 class="heading-section"><span>Список товаров</span></h2>
    <input v-model="searchQuery" placeholder="Фильтр по названию" class="width-50" />
    <select v-model="sortOrder" class="width-20">
      <option value="asc">Сортировать по возрастанию</option>
      <option value="desc">Сортировать по убыванию</option>
    </select>
    <button @click="fetchProducts" class="width-20">Обновить список</button>
    <button @click="showAddProductModal" class="width-20">Добавить товар</button>
    <ul class="width-100">
      <li v-for="product in filteredProducts" :key="product.id" class="width-30">
        <ProductItem :product="product" @delete="deleteProduct" @edit="openEditModal" />
      </li>
    </ul>
    <AddProductModal v-if="showAddModal" @close="closeAddModal" @add="addProduct" />
    <EditModal v-if="showEditModal" :product="currentProduct" @close="closeEditModal" @save="saveProduct" />
  </div>
</template>

<script>
import axios from 'axios';
import ProductItem from './ProductItem.vue';
import EditModal from './EditModal.vue';
import AddProductModal from './AddProductModal.vue';

export default {
  components: { ProductItem, EditModal, AddProductModal },
  data() {
    return {
      products: [],
      searchQuery: '',
      sortOrder: 'asc',
      showEditModal: false,
      showAddModal: false,
      currentProduct: null,
    };
  },
  computed: {
    filteredProducts() {
      let filtered = this.products.filter(product =>
        product.title.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
      if (this.sortOrder === 'asc') {
        filtered.sort((a, b) => a.title.localeCompare(b.title));
      } else {
        filtered.sort((a, b) => b.title.localeCompare(a.title));
      }
      return filtered;
    }
  },
  methods: {
    async fetchProducts() {
      const response = await axios.get('https://fakestoreapi.com/products');
      this.products = response.data;
    },
    async addProduct(product) {
      product.image = 'https://via.placeholder.com/150'; 
      const response = await axios.post('https://fakestoreapi.com/products', product);
      this.products.push(response.data);
      this.closeAddModal();
    },
    async deleteProduct(id) {
      await axios.delete(`https://fakestoreapi.com/products/${id}`);
      this.products = this.products.filter(product => product.id !== id);
    },
    openEditModal(product) {
      this.currentProduct = { ...product };
      this.showEditModal = true;
    },
    closeEditModal() {
      this.showEditModal = false;
      this.currentProduct = null;
    },
    saveProduct(updatedProduct) {
      const index = this.products.findIndex(product => product.id === updatedProduct.id);
      if (index !== -1) {
        this.products.splice(index, 1, updatedProduct);
      }
      this.closeEditModal();
    },
    showAddProductModal() {
      this.showAddModal = true;
    },
    closeAddModal() {
      this.showAddModal = false;
    }
  },
  mounted() {
    this.fetchProducts();
  }
};
</script>

<style scoped>
ul {
  list-style: none;
  padding: 0;
  display: flex;
  flex-wrap: wrap;
}

li {
  padding: 10px;
  margin: 10px;
  width: calc(33.33% - 20px);
}

@media (max-width: 768px) {
  li {
    width: calc(50% - 20px);
  }
}

@media (max-width: 480px) {
  li {
    width: 100%;
  }
}
</style>
