<script setup lang="ts">
import { ref } from 'vue';

const product = ref({
  id: 0,
  name: '',
  image: '',
  price: 0,
  quantity: 0
});

// Hàm thêm mới sản phẩm
const createProduct = async () => {
  try {
    const response = await fetch('http://localhost:3000/products', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(product.value)
    });

    if (!response.ok) {
      throw new Error('Network response was not ok');
    }

    const result = await response.json();
    console.log(result);
  } catch (error) {
    console.error('Failed to create product:', error);
  }
};

// Hàm xử lý sự kiện khi người dùng nhấn nút "Thêm mới"
const handleSubmit = (event: Event) => {
  event.preventDefault();
  createProduct();
};
</script>

<template>
  <div class="container">
    <h2>Thêm Sản Phẩm Mới</h2>
    <form @submit="handleSubmit" class="product-form">
      <div class="form-group">
        <label for="name">Tên sản phẩm</label>
        <br>
        <input type="text" id="name" v-model="product.name" required />
      </div>

      <div class="form-group">
        <label for="image">Hình ảnh (URL)</label>
        <br>
        <input type="text" id="image" v-model="product.image" required />
      </div>

      <div class="form-group">
        <label for="price">Giá sản phẩm</label>
        <br>
        <input type="number" id="price" v-model.number="product.price" required />
      </div>

      <div class="form-group">
        <label for="quantity">Số lượng</label>
        <br>
        <input type="number" id="quantity" v-model.number="product.quantity" required />
      </div>

      <button type="submit" class="btnAdd">Thêm mới</button>
    </form>
  </div>
</template>

<style scoped>
.container {
  max-width: 400px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 8px;
  background-color: #f9f9f9;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

h2 {
  text-align: center;
  margin-bottom: 20px;
  color: #333;
}

.product-form {
  display: flex;
  flex-direction: column;
}

.form-group {
  margin-bottom: 15px;
}

label {
  font-weight: bold;
  margin-bottom: 5px;
  color: #555;
}

input[type="text"],
input[type="url"],
input[type="number"] {
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 16px;
}

input:focus {
  border-color: #66afe9;
  outline: none;
}

.btnAdd {
  padding: 10px;
  background-color: #28a745;
  color: white;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.btnAdd:hover {
  background-color: #218838;
}

.btnAdd:active {
  background-color: #1e7e34;
}
</style>
