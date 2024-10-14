<template>
  <div class="flex p-4 space-x-2 bg-blue-500 text-white">
    <router-link to="/home" class="hover:text-gray-400">Home</router-link>
    <router-link to="/products" >Products</router-link>
   
  </div>

  <div>
    <router-view />
  </div>
</template>