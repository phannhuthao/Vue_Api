<script setup lang="ts">
// import { onMounted } from 'vue';
// import { ref } from 'vue';

const getProductById = async (id: number) => {
  try {
    const response = await fetch(`http://localhost:3000/products/${id}`);
    if (!response.ok) {
      console.log("Không tìm thấy bản ghi");
      return;
    }
    const product = await response.json();
    console.log(product);
  } catch (error) {
    console.error('Failed to fetch product:', error);
  }
};

const handleButtonClick = () => {
  const id = 1;
  getProductById(id);
};
</script>

<template>
  <button @click="handleButtonClick">Get Detail</button>
</template>

<style scoped>
</style>
