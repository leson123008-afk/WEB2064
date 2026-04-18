<template>
  <div class="container mt-4">
    <h1 class="text-center mb-4">Lab 6 - Vue.js Lifecycle Hooks & Axios</h1>
    
    <div class="mb-5">
      <h2>Bài 1: UserStatus - Theo dõi trạng thái Online/Offline</h2>
      <Bai1 />
    </div>

    <div class="mb-5">
      <h2>Bài 2: DataFetcher - Tải bài viết từ API</h2>
      <Bai2 />
    </div>

    <div class="mb-5">
      <h2>Bài 3: UserList - Danh sách người dùng</h2>
      <Bai3 />
    </div>

    <div class="mb-5">
      <h2>Bài 4: UserDashboard - Thêm người dùng mới</h2>
      <Bai4 />
    </div>
  </div>
</template>

<script setup>
import Bai1 from "./Labs/Lab-6/Bai1.vue";
import Bai2 from "./Labs/Lab-6/Bai2.vue";
import Bai3 from "./Labs/Lab-6/Bai3.vue";
import Bai4 from "./Labs/Lab-6/Bai4.vue";
</script>

<style scoped>
h1 {
  color: #333;
  margin-bottom: 30px;
}

h2 {
  color: #555;
  border-bottom: 2px solid #007bff;
  padding-bottom: 10px;
  margin-bottom: 20px;
  margin-top: 30px;
}

.mb-5 {
  margin-bottom: 3rem;
  padding: 20px;
  background-color: white;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}
</style>

