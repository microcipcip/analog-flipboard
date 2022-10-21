<script setup lang="ts">
import Flippy from './components/Flippy.vue'
</script>

<template>
  <div style="display: grid; grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr 1fr; gap: 2rem">
    <Flippy :index-to-stop="0" />
    <Flippy :start-index="9" :index-to-stop="8" :delay="130" />
    <Flippy :start-index="13" :index-to-stop="17" :delay="700" />
    <Flippy :start-index="24" :index-to-stop="19" :delay="400" />
    <Flippy :start-index="2" :index-to-stop="0" :delay="140" />
    <Flippy :start-index="2" :index-to-stop="12" :delay="340" />
    <Flippy :start-index="2" :index-to-stop="4" :delay="950" />
  </div>
</template>
