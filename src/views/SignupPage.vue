<template>
  <div class="signup-page">
    <div class="container py-5">
      <div class="row justify-content-center">
        <div class="col-md-6 col-lg-5">
          <div class="card shadow">
            <div class="card-body p-5">
              <h2 class="text-center mb-4">Create a New Account</h2>

              <div
                v-if="successMessage"
                class="alert alert-success"
                role="alert"
              >
                {{ successMessage }}
              </div>

              <div v-if="errorMessage" class="alert alert-danger" role="alert">
                {{ errorMessage }}
              </div>

              <form @submit.prevent="handleSignup">
                <div class="mb-3">
                  <label for="name" class="form-label">Name</label>
                  <input
                    type="text"
                    class="form-control"
                    id="name"
                    v-model="formData.name"
                    required
                    placeholder="Enter your name"
                  />
                </div>

                <div class="mb-3">
                  <label for="email" class="form-label">Email</label>
                  <input
                    type="email"
                    class="form-control"
                    id="email"
                    v-model="formData.email"
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
                    v-model="formData.password"
                    required
                    placeholder="Enter your password"
                    minlength="6"
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
                  {{ isLoading ? "Signing up..." : "Sign Up" }}
                </button>

                <div class="text-center">
                  <p class="mb-0">
                    Already have an account?
                    <router-link to="/login" class="text-decoration-none"
                      >Login</router-link
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

const router = useRouter();

const formData = ref({
  name: "",
  email: "",
  password: "",
});

const isLoading = ref(false);
const successMessage = ref("");
const errorMessage = ref("");

const handleSignup = async () => {
  isLoading.value = true;
  successMessage.value = "";
  errorMessage.value = "";

  try {
    const response = await fetch(
      "https://electronics-store-c9093-default-rtdb.firebaseio.com/Sign%20up.json",
      {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          name: formData.value.name,
          email: formData.value.email,
          password: formData.value.password,
          createdAt: new Date().toISOString(),
        }),
      }
    );

    if (response.ok) {
      successMessage.value =
        "Account created successfully! Redirecting to login page...";
      formData.value = { name: "", email: "", password: "" };

      setTimeout(() => {
        router.push("/login");
      }, 2000);
    } else {
      errorMessage.value =
        "An error occurred while creating the account. Please try again.";
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
.signup-page {
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
