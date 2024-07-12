<template>
  <div id="app">
    <header>
      <div class="container">
        <h1>Онлайн магазин</h1>
      </div>
    </header>
    <main>
      <div class="container">
        <ProductList />
      </div>
    </main>
    <footer>
      <div class="container">
        <p>&copy; 2024 Онлайн магазин. Все права защищены.</p>
      </div>
    </footer>
  </div>
</template>

<script>
import ProductList from './components/ProductList.vue';

export default {
  name: 'App',
  components: {
    ProductList
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Roboto', sans-serif;
  font-size: 14px;
  color: #242424;
  font-weight: 400;
}

.container {
  max-width: 1150px;
  margin: 0 auto;
  padding: 0 20px;
}

header,
footer {
  background-color: #333;
  color: #fff;
  padding: 20px 0;
  text-align: center;
}

footer {
  margin-top: 40px;
}

button {
  padding: 10px 20px;
  background-color: #787eff;
  color: #fff;
  border: none;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #5555ff;
}

input,
textarea,
select {
  padding: 10px;
  border: 1px solid #ccc;
  font-size: 14px;
  width: 100%;
  margin-bottom: 10px;
  box-sizing: border-box;
}

input:focus,
textarea:focus,
select:focus {
  border-color: #787eff;
  outline: none;
  box-shadow: 0 0 5px rgba(120, 126, 255, 0.5);
}


/* Медиа-запросы */
@media (max-width: 768px) {
  .container {
    padding: 0 10px;
  }
}

@media (max-width: 480px) {
  .container {
    padding: 0 5px;
  }
}
</style>
