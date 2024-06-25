<script setup lang="ts">
const username = defineModel('username', {})
const password = defineModel('password', {})

const emit = defineEmits(
    {
      submit: ({username, password}) => {
        if (username && password) return true;
        else {
          console.log("email and password must be provided")
          return false;
        }
      }
    }
)

const handleLogin = () => {
  emit('submit', {username, password})
}

</script>
<template>
  <form @submit.prevent="handleLogin">
    <h1>Login</h1>
    <label>
      <span>Username</span>
      <input type="text" v-model="username"/>
    </label>

    <label>
      <span>Password</span>
      <input type="password" v-model="password"/>
    </label>

    <button>Login</button>
  </form>
</template>
