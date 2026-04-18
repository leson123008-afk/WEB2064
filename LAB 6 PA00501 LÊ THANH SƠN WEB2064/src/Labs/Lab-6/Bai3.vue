<template>
  <div class="container mt-4">
    <button class="btn btn-primary mb-3" @click="fetchData">Tải người dùng</button>
    <div v-if="loading" class="alert alert-info">Đang tải dữ liệu...</div>
    <div class="row">
      <div v-for="user in users" :key="user.id" class="col-md-4 mb-3">
        <div class="card">
          <div class="card-body">
            <h5 class="card-title">{{ user.name }}</h5>
            <h6 class="card-subtitle mb-2 text-muted">{{ user.email }}</h6>
            <p class="card-text">
              Địa chỉ: {{ user.address.street }}, {{ user.address.city }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onBeforeUpdate, onUpdated } from "vue";
import axios from "axios";

const users = ref([]);
const loading = ref(false);

const fetchData = async () => {
  loading.value = true;
  const response = await axios.get("http://localhost:3000/users");
  users.value = response.data;
  loading.value = false;
};

onBeforeUpdate(() => {
  console.log("Component sẽ cập nhật.");
});

onUpdated(() => {
  console.log("Component đã cập nhật.");
});
</script>

<style scoped>
.row {
  display: flex;
  flex-wrap: wrap;
  margin: 0 -15px;
}

.col-md-4 {
  flex: 0 0 33.333333%;
  max-width: 33.333333%;
  padding: 0 15px;
}

@media (max-width: 768px) {
  .col-md-4 {
    flex: 0 0 100%;
    max-width: 100%;
  }
}

.alert-info {
  color: #0c5460;
  background-color: #d1ecf1;
  border-color: #bee5eb;
}
</style>

