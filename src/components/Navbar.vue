<script setup>
import router from "../router";
import { useAuth } from "../stores/auth";
import { ElMessage, ElNotification } from "element-plus";

const auth = useAuth();
function logOut() {
  const success = auth.logout();
  if (success) {
    router.push({ name: "login" });
    ElNotification({
      title: "Success",
      message: "You have Successfully Logged Out",
      type: "success",
      position: "top-right",
      duration: 2000,
    });
  } else {
    ElMessage({
      type: "error",
      message: "Something went wrong",
    });
  }
}

import { ref } from "vue";

const mobileMenuOpen = ref(false);

const toggleMobileMenu = () => {
  mobileMenuOpen.value = !mobileMenuOpen.value;
};
</script>

<template>
  <nav
    class="bg-slate-900 z-50 sticky top-0 shadow-lg border-b border-b-slate-500"
  >
    <div class="flex justify-between items-center p-4">
      <div class="flex justify-between items-center space-x-5">
        <RouterLink :to="{ name: 'dashboard' }" class="flex items-center">
          <h2 class="text-3xl text-white">ComLogo</h2>
        </RouterLink>

        <button @click="toggleMobileMenu" class="focus:outline-none">
          <svg
            v-show="!mobileMenuOpen"
            class="w-6 h-6"
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 24 24"
            fill="none"
            stroke="white"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
          >
            <path d="M3 12h18M3 6h18M3 18h18"></path>
          </svg>

          <svg
            v-show="mobileMenuOpen"
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="white"
            class="w-6 h-6"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M6 18L18 6M6 6l12 12"
            />
          </svg>
        </button>
      </div>

      <div class="flex items-center space-x-2">
        <a href="#" class="relative p-1">
          <div class="absolute right-0 -top-0">
            <span class="relative flex h-3 w-3">
              <span
                class="animate-ping absolute inline-flex h-full w-full rounded-full bg-slate-400 opacity-75"
              ></span>
              <span
                class="relative inline-flex rounded-full h-3 w-3 bg-slate-500"
              ></span>
            </span>
          </div>
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="white"
            class="w-6 h-6"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M14.857 17.082a23.848 23.848 0 005.454-1.31A8.967 8.967 0 0118 9.75v-.7V9A6 6 0 006 9v.75a8.967 8.967 0 01-2.312 6.022c1.733.64 3.56 1.085 5.455 1.31m5.714 0a24.255 24.255 0 01-5.714 0m5.714 0a3 3 0 11-5.714 0M3.124 7.5A8.969 8.969 0 015.292 3m13.416 0a8.969 8.969 0 012.168 4.5"
            />
          </svg>
        </a>

        <div class="dropdown inline-block relative">
          <button
            class="bg-slate-700 text-white font-semibold py-2 px-4 rounded inline-flex space-x-2 items-center"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="white"
              class="w-6 h-6"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M17.982 18.725A7.488 7.488 0 0012 15.75a7.488 7.488 0 00-5.982 2.975m11.963 0a9 9 0 10-11.963 0m11.963 0A8.966 8.966 0 0112 21a8.966 8.966 0 01-5.982-2.275M15 9.75a3 3 0 11-6 0 3 3 0 016 0z"
              />
            </svg>
            <span>Akhi</span>
          </button>
          <ul
            class="dropdown-menu absolute hidden text-center border bg-slate-500 text-slate-300 p-1"
          >
            <li class="">
              <a
                class="border-b border-dotted py-2 px-4 block whitespace-no-wrap"
                href="#"
                >Profile</a
              >
            </li>
            <li class="">
              <a
                class="rounded-t border-b border-dotted py-2 px-4 block whitespace-no-wrap"
                href="#"
                >Dashboard</a
              >
            </li>

            <li class="">
              <a
                href="#"
                @click.prevent="logOut()"
                class="rounded-t py-2 px-4 block whitespace-no-wrap"
              >
                Log Out
              </a>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </nav>
</template>

<style scoped>
.dropdown:hover .dropdown-menu {
  display: block;
}
</style>
