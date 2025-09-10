<template>
<div class="center">
<n-card :bordered="false" size="large" style="width: 640px; max-width: 100%; box-shadow: 0 8px 30px rgba(0,0,0,.06)">
<n-space vertical :size="16">
<n-h1 style="text-align:center; margin: 0;">骰子投掷（时间种子随机）</n-h1>
<DiceRoller />
</n-space>
</n-card>
</div>
</template>


<script setup lang="ts">
import { NH1, NCard, NSpace } from 'naive-ui'
import DiceRoller from './components/DiceRoller.vue'
</script>


<style>
html, body, #app { height: 100%; }
body { margin: 0; background: #f5f7fa; font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Helvetica, Arial, "Apple Color Emoji", "Segoe UI Emoji"; }
.center { min-height: 100%; display: grid; place-items: center; padding: 24px; }
</style>