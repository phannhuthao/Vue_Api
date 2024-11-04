<script setup lang="ts">
import { onMounted } from 'vue';

const getAllProduct = async () => {
  try {
    const response = await fetch('http://localhost:3000/products');
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    const data = await response.json();
    console.log(data.product);
  } catch (error) {
    console.error('Failed to fetch products:', error);
  }
};

onMounted(() => {
  getAllProduct();
});
</script>

<template>
</template>

<style scoped>
</style>
