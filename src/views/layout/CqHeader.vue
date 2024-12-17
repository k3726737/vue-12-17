<template>
  <!-- QHeader 支援動態背景顏色 -->
  <q-header elevated class="glossy" :style="{ backgroundColor: bgColor }">
    <q-toolbar>
      <!-- 切換 Menu 功能 -->
      <q-btn
        flat
        dense
        round
        @click="switchMenu"
        aria-label="Menu"
        icon="menu"
      />

      <!-- 標題 -->
      <q-toolbar-title> Quasar App </q-toolbar-title>

      <!-- Quasar 版本 -->
      <div>Quasar v{{ $q.version }}</div>

      <!-- 背景顏色更改按鈕 -->
      <q-btn
        flat
        dense
        round
        color="primary"
        label="更改背景顏色"
        @click="changeBgColor"
      />
    </q-toolbar>
  </q-header>
</template>

<script setup lang="ts">
import { defineProps, toRef, defineEmits, ref } from 'vue'

// Props 定義
const props = defineProps({
  leftDrawerOpen: {
    type: Boolean,
    default: false
  }
})

// Emits
const emit = defineEmits(['update:leftDrawerOpen'])

// 響應式變數
const leftDrawerOpen = toRef(props, 'leftDrawerOpen')

// 背景顏色變數
const bgColor = ref('#4CAF50') // 初始顏色（Quasar 藍色）

// 切換左側選單
const switchMenu = () => {
  emit('update:leftDrawerOpen', !leftDrawerOpen.value)
}

// 更改背景顏色（隨機色）
const changeBgColor = () => {
  const randomColor = `#${Math.floor(Math.random() * 16777215).toString(16)}`
  bgColor.value = randomColor
}
</script>
<!-- 注意lang="scss" -->
<style lang="scss">
div {
  color: $brown-8;
}
</style>
<style scoped>
/* 可額外自訂其他樣式 */
</style>
