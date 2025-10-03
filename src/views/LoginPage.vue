<template>
  <div class="login-page">
    <div class="container py-5">
      <div class="row justify-content-center">
        <div class="col-md-6 col-lg-5">
          <div class="card shadow">
            <div class="card-body p-5">
              <h2 class="text-center mb-4">Sign in</h2>

              <div v-if="errorMessage" class="alert alert-danger" role="alert">
                {{ errorMessage }}
              </div>

              <form @submit.prevent="handleLogin">
                <div class="mb-3">
                  <label for="email" class="form-label">Email</label>
                  <input
                    type="email"
                    class="form-control"
                    id="email"
                    v-model="loginData.email"
                    required
                    placeholder="Enter your email"
                  />
                </div>

                <div class="mb-3">
                  <label for="password" class="form-label">Password</label>
                  <input
                    type="password"
                    class="form-control"
                    id="password"
                    v-model="loginData.password"
                    required
                    placeholder="Enter your password"
                  />
                </div>

                <button
                  type="submit"
                  class="btn btn-primary w-100 mb-3"
                  :disabled="isLoading"
                >
                  <span
                    v-if="isLoading"
                    class="spinner-border spinner-border-sm me-2"
                  ></span>
                  {{ isLoading ? "Signing in..." : "Login" }}
                </button>

                <div class="text-center">
                  <p class="mb-0">
                    Don’t have an account?
                    <router-link to="/signup" class="text-decoration-none"
                      >Create a new account</router-link
                    >
                  </p>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { useRouter } from "vue-router";
import { useAuthStore } from "../store/authStore";

const router = useRouter();
const authStore = useAuthStore();

const loginData = ref({
  email: "",
  password: "",
});

const isLoading = ref(false);
const errorMessage = ref("");

const handleLogin = async () => {
  isLoading.value = true;
  errorMessage.value = "";

  try {
    const response = await fetch(
      "https://electronics-store-c9093-default-rtdb.firebaseio.com/Sign%20up.json"
    );

    if (!response.ok) {
      throw new Error("Failed to connect to the server");
    }

    const users = await response.json();

    let userFound = false;
    let userData = null;

    if (users) {
      for (const key in users) {
        const user = users[key];
        if (
          user.email === loginData.value.email &&
          user.password === loginData.value.password
        ) {
          userFound = true;
          userData = {
            id: key,
            name: user.name,
            email: user.email,
          };
          break;
        }
      }
    }

    if (userFound) {
      authStore.login(userData);
      router.push("/");
    } else {
      errorMessage.value = "Incorrect email or password";
    }
  } catch (error) {
    errorMessage.value =
      "A connection error occurred. Please check your internet connection.";
  } finally {
    isLoading.value = false;
  }
};
</script>

<style scoped>
.login-page {
  min-height: calc(100vh - 200px);
  display: flex;
  align-items: center;
  background-color: #f8f9fa;
}

.card {
  border: none;
  border-radius: 15px;
}

.btn-primary {
  padding: 12px;
  font-size: 1.1rem;
  border-radius: 8px;
}
</style>
