<script setup>
import { ref } from 'vue'

const gridRows = ref(8)
const gridCols = ref(10)
</script>

<template>

  <div class="bgGrid">
    <div class="Grid right">
      <div class="mask"></div>
      <div class="itemGrid-row" v-for="i in gridRows" :key="i">
        <div class="itemGrid-cols" v-for="j in gridCols" :key="j"></div>
      </div>
    </div>

    <div class="Grid left">
      <div class="mask"></div>
      <div class="itemGrid-row" v-for="i in gridRows" :key="i">
        <div class="itemGrid-cols" v-for="j in gridCols" :key="j"></div>
      </div>
    </div>
  </div>


  <router-view></router-view>
</template>

<style></style>