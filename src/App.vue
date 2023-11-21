<script setup lang="ts">
import { useRouter } from "vue-router";
import { useAuthStore } from "@/stores/auth";

// access the `store` variable anywhere in the component ✨
const auth = useAuthStore();
const router = useRouter();

const onLogout = () => {
  auth.logout();
  router.push("/login");
};
</script>

<template>
  <div class="flex flex-col container mx-auto p-4 gap-10">
    <!--Header-->
    <div class="flex justify-between">
      <!--Menu-->
      <div class="flex gap-4">
        <router-link to="/">Home</router-link>
        <router-link to="/about">About</router-link>
        <router-link to="/restricted">Restricted Page</router-link>
      </div>
      <!--Authenticated User-->
      <div>
        <p v-if="auth.username">{{ auth.username }}</p>
        <div v-if="auth.username">
          <button class="btn" to="/login" @click="onLogout()">Logout</button>
        </div>

        <div v-else>
          <router-link class="btn" to="/login">Login</router-link>
        </div>
      </div>
    </div>
    <!--Body-->
    <router-view></router-view>
  </div>
</template>
