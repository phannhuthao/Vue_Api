<script setup lang="ts">
const removeProductById = async (id: number) => {
  try {
    const response = await fetch(`http://localhost:3000/products/${id}`, {
      method: 'DELETE',
    });

    if (!response.ok) {
      console.log("Lỗi không xóa sản phẩm");
      return;
    }

    const result = await response.json();
    console.log("Xóa sản phẩm:", result);
  } catch (error) {
    console.error("Lỗi không xóa sản phẩm:", error);
  }
};

const handleDeleteClick = () => {
  const productId = 1;
  removeProductById(productId);
};
</script>

<template>
  <button @click="handleDeleteClick">Delete</button>
</template>

<style scoped>
</style>
