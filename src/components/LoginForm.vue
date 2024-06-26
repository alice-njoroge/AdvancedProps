<script setup lang="ts">
import {ref, watch} from "vue";

const props = defineProps({
  modelValue: {
    type: Object,
    default() {
      return {username: '', password: ''}
    },
  }
});

const clone = (obj: any) => {
  return JSON.parse(JSON.stringify(obj))
};

const localObj = ref();

watch(
    () => props.modelValue,
    (newValue) => {
      localObj.value = clone(newValue);
    },
    { immediate: true },
);


const emit = defineEmits(
    {
      'update:modelValue': ({username, password}) => {
        if (username && password) return true;
        else {
          console.log("email and password must be provided")
          return false;
        }
      }
    }
)

const handleLogin = () => {
  emit('update:modelValue', clone(localObj.value))
}

</script>
<template>
  <form @submit.prevent="handleLogin">
    <h1>Login</h1>
    <label>
      <span>Username</span>
      <input type="text" v-model="localObj.username"/>
    </label>

    <label>
      <span>Password</span>
      <input type="password" v-model="localObj.password"/>
    </label>

    <button>Login</button>
  </form>
</template>
