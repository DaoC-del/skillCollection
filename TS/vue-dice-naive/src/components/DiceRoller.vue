<template>
<n-space vertical :size="16" style="width: 100%">
<!-- 结果显示区（X-Y） -->
<n-card :segmented="{ content: true }" title="结果">
<div class="result" aria-live="polite">{{ result || '--' }}</div>
</n-card>


<!-- 骰子图标区 -->
<div class="dice-row">
<div class="die" :class="{ rolling }">{{ face(die1) }}</div>
<div class="die" :class="{ rolling }">{{ face(die2) }}</div>
</div>


<!-- 种子信息 -->
<div class="seed">时间种子：{{ seed || '未生成' }}</div>


<!-- 操作区 -->
<n-space justify="center">
<n-button type="primary" size="large" :loading="rolling" @click="roll">投掷两个色子</n-button>
<n-button quaternary @click="clearAll">清空</n-button>
</n-space>
</n-space>
</template>


<script setup lang="ts">
import { ref } from 'vue'
import { NButton, NCard, NSpace } from 'naive-ui'
import seedrandom from 'seedrandom'


const result = ref<string>('')
const seed = ref<string>('')
const die1 = ref<number | null>(null)
const die2 = ref<number | null>(null)
const rolling = ref<boolean>(false)


const faces = ['', '⚀', '⚁', '⚂', '⚃', '⚄', '⚅'] as const
const face = (n: number | null) => (n ? faces[n] : '🎲')


function d6(r: () => number): number {
return Math.floor(r() * 6) + 1
}


function roll() {
rolling.value = true
// 给一点动画时间再落点
setTimeout(() => {
seed.value = new Date().toISOString()
const rng = seedrandom(seed.value)
const x = d6(rng)
const y = d6(rng)
die1.value = x
die2.value = y
result.value = `${x}-${y}`
rolling.value = false
}, 500)
}


function clearAll() {
result.value = ''
seed.value = ''
die1.value = null
die2.value = null
}
</script>


<style scoped>
.result { font-size: 40px; font-weight: 800; letter-spacing: .2em; text-align: center; }
.dice-row { display: flex; gap: 24px; justify-content: center; align-items: center; }
.die { font-size: 72px; filter: drop-shadow(0 6px 12px rgba(0,0,0,.1)); transition: transform .4s; }
.die.rolling { animation: jiggle .5s ease-in-out infinite; }
@keyframes jiggle { 0% { transform: rotate(0deg) translateY(0); } 50% { transform: rotate(10deg) translateY(-2px); } 100% { transform: rotate(-10deg) translateY(0); } }
.seed { margin-top: 4px; text-align: center; font-size: 12px; color: #909399; }
</style>