<template>
  <q-drawer v-if="leftDrawerOpen" show-if-above bordered :style="{ backgroundColor: backgroundColor }">
    <q-list>
      <q-item-label header>Essential Links</q-item-label>

      <!-- 使用 v-for 動態生成項目 -->
      <q-item
        v-for="item in menuItems"
        :key="item.name"
        clickable
        tag="router-link"
        :to="{ name: item.route }"
      >
        <q-item-section avatar>
          <q-icon :name="item.icon" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ item.label }}</q-item-label>
          <q-item-label caption>{{ item.caption }}</q-item-label>
        </q-item-section>
      </q-item>
    </q-list>

    <!-- 背景顏色切換按鈕 -->
    <!-- <q-btn label="Change Background" @click="changeBackgroundColor" color="primary" class="q-mt-md" /> -->
  </q-drawer>
</template>

<script setup lang="ts">
import { defineProps, toRef, ref } from 'vue'

// 定義 props
const props = defineProps({
  leftDrawerOpen: Boolean
})

const leftDrawerOpen = toRef(props, 'leftDrawerOpen')

// 動態項目資料
const menuItems = ref([
  { name: 'home', route: 'home', icon: 'home', label: '首頁', caption: 'Home page' },
  { name: 'product-list', route: 'product-list', icon: 'description', label: '產品列表', caption: 'product-list' },
  { name: 'create-product', route: 'create-product', icon: 'dashboard_customize', label: '產品建立', caption: 'create-product' },
  { name: 'user-info', route: 'user-info', icon: 'perm_identity', label: '個人資訊', caption: 'user info' },
  { name: 'api-test', route: 'api-test', icon: 'rss_feed', label: 'Api 獲取', caption: 'Api fetch test' },
  { name: 'address-select', route: 'address-select', icon: 'switch_access_shortcut', label: '位置獲取', caption: 'address-select' }
])

// 動態背景顏色
const backgroundColor = ref('#ADD8E6') // 預設綠色

// 切換背景顏色的功能
const changeBackgroundColor = () => {
  const colors = ['#4CAF50', '#FF5722', '#2196F3', '#9C27B0', '#FFC107']
  const randomIndex = Math.floor(Math.random() * colors.length)
  backgroundColor.value = colors[randomIndex]
}
</script>
