<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import { login } from '../auth'

const username = ref('')
const password = ref('')
const errorMsg = ref('')
const router = useRouter()

const performLogin = () => {
  if (login(username.value, password.value)) {
    errorMsg.value = ''
    router.push('/about')
  } else {
    errorMsg.value = 'Invalid credentials (Use: admin / Password123%)'
  }
}
</script>

<template>
  <div class="container mt-5">
    <div class="row">
      <div class="col-md-6 offset-md-3">
        <h2 class="text-center mb-4">Login</h2>
        <form @submit.prevent="performLogin">
          <div class="mb-3">
            <label class="form-label">Username</label>
            <input type="text" class="form-control" v-model="username" required />
          </div>
          <div class="mb-3">
            <label class="form-label">Password</label>
            <input type="password" class="form-control" v-model="password" required />
          </div>
          <div v-if="errorMsg" class="text-danger small mb-3">{{ errorMsg }}</div>
          <button type="submit" class="btn btn-primary w-100">Login</button>
        </form>
      </div>
    </div>
  </div>
</template>
