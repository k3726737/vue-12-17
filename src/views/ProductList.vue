<template>
  <q-page padding>
    <!-- 標題工具欄 -->
    <q-toolbar>
      <q-toolbar-title>產品列表</q-toolbar-title>
      <q-btn label="新增產品" color="primary" @click="addProduct" />
    </q-toolbar>

    <!-- 篩選條件 -->
    <div class="q-mb-md">
      <q-toggle
        v-model="showInStock"
        label="只顯示有庫存產品"
        color="primary"
      />
    </div>

    <!-- 卡片區域 -->
    <div class="row q-col-gutter-md q-mt-md">
      <div
        class="col-xs-12 col-sm-6 col-md-4"
        v-for="product in filteredProducts"
        :key="product.id"
      >
        <q-card>
          <!-- 卡片內容 -->
          <q-card-section>
            <div class="text-h6">{{ product.name }}</div>
            <div class="text-subtitle2 text-positive">
              價格：NTD {{ product.price.toFixed(2) }}
            </div>
          </q-card-section>

          <!-- 額外資訊 -->
          <q-card-section>
            <q-chip
              color="blue"
              text-color="white"
              outline
              v-if="product.category"
              class="q-mr-sm"
            >
              類別：{{ product.category }}
            </q-chip>
            <q-chip
              :color="product.inStock ? 'green' : 'red'"
              text-color="white"
              outline
            >
              {{ product.inStock ? "有庫存" : "缺貨" }}
            </q-chip>
          </q-card-section>

          <!-- 卡片操作 -->
          <q-card-actions align="right">
            <q-btn
              label="編輯"
              color="primary"
              flat
              @click="editProduct(product.id)"
            />
            <q-btn
              label="刪除"
              color="negative"
              flat
              @click="deleteProduct(product.id)"
            />
          </q-card-actions>
        </q-card>
      </div>
    </div>
  </q-page>
</template>

<script>
import { ref, computed } from 'vue'

export default {
  setup () {
    const products = ref([
      { id: 1, name: '自動攝影機', price: 2899, category: '電子產品', inStock: true },
      { id: 2, name: '液晶螢幕', price: 18299, category: '電子產品', inStock: true },
      { id: 3, name: '電熱毯', price: 816, category: '家居用品', inStock: false },
      { id: 4, name: '微波爐', price: 1932, category: '電子產品', inStock: false },
      { id: 5, name: '羊毛衫', price: 1209, category: '服飾', inStock: true },
      { id: 6, name: '保溫器', price: 2376, category: '家居用品', inStock: false },
      { id: 7, name: '電競筆記型電腦', price: 29312, category: '電子產品', inStock: false },
      { id: 8, name: '陽綠雪球圓潤翡翠', price: 12059, category: '戒指', inStock: true },
      { id: 9, name: '春帶彩初綠飄花', price: 31376, category: '手鐲', inStock: false },
      { id: 10, name: '冰藍花甜甜圈墜飾18K', price: 19352, category: '項鍊', inStock: false },
      { id: 11, name: '冰晴圓珠耳針18K', price: 19305, category: '耳環', inStock: false },
      { id: 12, name: '紫飄花愛心手鍊18K', price: 9384, category: '手鍊', inStock: true },
      { id: 13, name: '幽深湖水綠', price: 24531, category: '戒指', inStock: false },
      { id: 14, name: '半山水黑豫圓骨鐲', price: 5123, category: '手鐲', inStock: true },
      { id: 15, name: '紫羅蘭珠串', price: 34562, category: '手鍊', inStock: true },
      { id: 16, name: '白冰戒圈', price: 27384, category: '戒指', inStock: true },
      { id: 17, name: '半山水老藍水戒圈', price: 62123, category: '戒指', inStock: true },
      { id: 18, name: '高冰近玻璃精品串', price: 72631, category: '手鍊', inStock: true }
    ])

    const showInStock = ref(false)

    // 過濾顯示的產品
    const filteredProducts = computed(() => {
      return showInStock.value
        ? products.value.filter(product => product.inStock)
        : products.value
    })

    const addProduct = () => {
      alert('新增產品功能尚未實作！')
    }

    const editProduct = id => {
      alert(`正在編輯產品 ID: ${id}`)
    }

    const deleteProduct = id => {
      alert(`產品 ID: ${id} 已刪除`)
    }

    return {
      products,
      showInStock,
      filteredProducts,
      addProduct,
      editProduct,
      deleteProduct
    }
  }
}
</script>

<style scoped>
.row {
  display: flex;
  flex-wrap: wrap;
}
</style>
