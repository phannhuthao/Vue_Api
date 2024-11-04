<template>
  <button class="btnAdd">Thêm mới sản phẩm</button>

  <table class="table">
    <thead>
    <tr>
      <th>#</th>
      <th>Tên Sản Phẩm</th>
      <th>Hình Ảnh</th>
      <th>Giá</th>
      <th>Số Lượng (Kg)</th>
      <th colspan="2">Chức Năng</th>
    </tr>
    </thead>
    <tbody>
    <tr v-for="(product, index) in products" :key="product.id">
      <td>{{ index + 1 }}</td>
      <td>{{ product.name }}</td>
      <td><img :src="product.image" alt="Product Image" width="100"/></td>
      <td>{{ product.price }}</td>
      <td>{{ product.quantity }}</td>
      <td>
        <button class="btnEdit">Sửa</button>
        <button class="btnDelete">Xóa</button>
      </td>
    </tr>
    </tbody>
  </table>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';

interface Product {
  id: number;
  name: string;
  image: string;
  price: number;
  quantity: number;
}

const products = ref<Product[]>([]);

onMounted(async () => {
  try {
    const response = await fetch('http://localhost:3000/products');
    const data = await response.json();
    console.log(data.products);
    products.value = data.products;
  } catch (error) {
    console.error('Error fetching data:', error);
  }
});
</script>

<style scoped>
.table {
  border: 1px solid #ddd;
  border-radius: 4px;
  width: 100%;
  margin-top: 20px;
  border-collapse: collapse;
}

.table th,
.table td {
  padding: 12px 15px;
  text-align: left;
  border-bottom: 1px solid #ddd;
}

.table th {
  background-color: #f5f5f5;
  font-weight: bold;
}

.btnEdit {
  background-color: orange;
  color: white;
  border: none;
  cursor: pointer;
}

.btnDelete {
  background-color: red;
  color: white;
  border: none;
  cursor: pointer;
}

.btnAdd {
  background-color: #3b82f6;
  color: white;
  border: none;
  padding: 5px 10px;
  border-radius: 4px;
  cursor: pointer;
  height: 35px;
  width: 150px;
}

.btnEdit,
.btnDelete {
  padding: 5px 10px;
  border-radius: 4px;
  cursor: pointer;
  margin-right: 5px;
}
</style>
