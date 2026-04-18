<template>
  <div class="user-dashboard">
    <h1>Thêm người dùng</h1>
    <!-- Form thêm người dùng mới -->
    <form @submit.prevent="addUser">
      <div class="form-group">
        <label for="name">Tên:</label>
        <input type="text" v-model="newUser.name" class="form-control" required />
      </div>
      <div class="form-group">
        <label for="email">Email:</label>
        <input type="email" v-model="newUser.email" class="form-control" required />
      </div>
      <div class="form-group">
        <label for="password">Mật khẩu:</label>
        <input type="password" v-model="newUser.password" class="form-control" required />
      </div>
      <button type="submit" class="btn btn-primary">Thêm người dùng</button>
    </form>

    <h2>Danh sách người dùng</h2>
    <ul>
      <li v-for="user in users" :key="user.id">{{ user.name }} - {{ user.email }}</li>
    </ul>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";

const users = ref([]); // Danh sách người dùng
const newUser = ref({ name: "", email: "", password: "" }); // Thông tin người dùng mới

// Hàm gọi API để lấy danh sách người dùng
const fetchUsers = async () => {
  try {
    const response = await axios.get("http://localhost:3000/users");
    users.value = response.data;
  } catch (error) {
    console.error("Có lỗi khi lấy danh sách người dùng:", error);
  }
};

// Hàm thêm người dùng mới
const addUser = async () => {
  try {
    // Tạo object user với đầy đủ thông tin cần thiết
    const userData = {
      name: newUser.value.name,
      email: newUser.value.email,
      password: newUser.value.password,
      address: {
        street: "",
        city: ""
      },
      phone: "",
      website: ""
    };
    
    // POST vào /users (json-server tự động tạo endpoint này)
    await axios.post("http://localhost:3000/users", userData);
    
    // Sau khi thêm thành công, fetch lại danh sách để có ID mới nhất
    await fetchUsers();
    newUser.value = { name: "", email: "", password: "" }; // Reset form
    alert("Thêm người dùng thành công!");
  } catch (error) {
    console.error("Có lỗi khi thêm người dùng:", error);
    if (error.code === 'ECONNREFUSED') {
      alert("Không thể kết nối đến server. Vui lòng chạy json-server:\n\nnpm run json-server\n\nhoặc\n\njson-server --watch db.json");
    } else {
      alert("Có lỗi khi thêm người dùng: " + (error.response?.data?.message || error.message));
    }
  }
};

onMounted(() => {
  fetchUsers();
});
</script>

