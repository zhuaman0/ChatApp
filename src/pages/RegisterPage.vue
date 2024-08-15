<template>
  <div class="body">
    <div class="main-container">
      <h1>Register</h1>
      <form class="main-form" @submit.prevent="handleSubmit">
        <input v-model="name" type="text" placeholder="Name" />
        <input v-model="surname" type="text" placeholder="Surname" />
        <input v-model="password" type="password" placeholder="Password" />
        <button type="submit">Submit</button>
        <div class="info">
          <p>Already have an account?</p>
          <b @click="goToLogin">Sign in</b>
        </div>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { useRouter } from "vue-router";

const router = useRouter();
const name = ref("");
const surname = ref("");
const password = ref("");

const handleSubmit = () => {
  // Handle registration logic here
  router.push("/main");
};

const goToLogin = () => {
  router.push("/login");
};
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.body {
  background-color: #f5f5f5;
  width: 100%;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.main-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: white;
  padding: 40px;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  width: 100%;
  max-width: 400px;
}

.main-container h1 {
  font-size: 28px;
  margin-bottom: 20px;
  color: #333;
}

.main-form {
  display: flex;
  flex-direction: column;
  width: 100%;
}

.main-form input {
  background-color: #f9f9f9;
  border: 1px solid #ddd;
  padding: 15px;
  margin: 10px 0;
  border-radius: 5px;
  width: 100%;
  font-size: 16px;
}

.main-form button {
  background-color: #007bff;
  border: none;
  color: white;
  padding: 15px;
  margin: 10px 0;
  border-radius: 5px;
  width: 100%;
  font-size: 16px;
  cursor: pointer;
}

.main-form button:hover {
  background-color: #0056b3;
}

.info {
  display: flex;
  gap: 5px;
  justify-content: center;
  font-size: 14px;
  color: #666;
}

.info b {
  color: #007bff;
  cursor: pointer;
}
</style>
