<template>
  <q-page class="q-pa-md" :style="backgroundStyle">
    <!-- 歡迎區塊 -->
    <q-banner class="q-mb-md" color="primary" text-color="white">
      <div class="text-h6">歡迎來到我們的商店！</div>
      <div>這裡是您瀏覽本月活動和查看商品資訊的地方。</div>
    </q-banner>

    <!-- 主要功能區塊 -->
    <div class="q-gutter-md">
      <div class="row">
        <div
          v-for="(feature, index) in featureList"
          :key="index"
          class="col-12 col-md-6"
        >
          <q-card>
            <q-card-section>
              <div class="text-h6">{{ feature.title }}</div>
              <p>{{ feature.description }}</p>
            </q-card-section>
            <q-card-actions>
              <q-btn
                :label="feature.buttonLabel"
                color="primary"
                flat
                @click="goToFeature(feature.id)"
              />
            </q-card-actions>
          </q-card>
        </div>
      </div>
    </div>

    <!-- 最新資訊區塊 -->
    <div class="q-mt-md">
      <q-card>
        <q-card-section>
          <div class="text-h6">最新資訊</div>
          <q-separator />
          <q-list>
            <q-item
              v-for="(news, index) in newsList"
              :key="index"
              clickable
            >
              <q-item-section>
                <div class="text-body1">{{ news.title }}</div>
                <div class="text-caption">{{ news.date }}</div>
              </q-item-section>
            </q-item>
          </q-list>
        </q-card-section>
      </q-card>
    </div>
  </q-page>
</template>

<script>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

export default {
  setup () {
    const router = useRouter()

    // 主要功能區塊列表
    const featureList = ref([
      {
        id: '1',
        title: '熱門商品',
        description: '本店目前提供優惠折扣和登上銷售排行的暢銷商品都在此列!',
        buttonLabel: '查看詳細'
      },
      {
        id: '2',
        title: '本月促銷',
        description: '隨著季節的變化新增的限時商品和搶購活動都不容錯過',
        buttonLabel: '查看詳細'
      }
    ])

    // 最新資訊列表
    const newsList = ref([
      { title: '系統更新公告', date: '2024-12-08' },
      { title: '新功能介紹', date: '2024-12-01' },
      { title: '用戶協議更新', date: '2024-11-25' }
    ])

    // 功能區塊跳轉
    const goToFeature = (featureId) => {
      console.log(`跳轉到功能區塊 ${featureId}`)
    }

    // 背景圖片樣式
    const backgroundStyle = {
      backgroundImage: 'url(../image/image1.jpg)', // 請根據實際圖片路徑修改
      backgroundSize: 'cover',
      backgroundPosition: 'center center',
      backgroundRepeat: 'no-repeat'
    }

    return {
      featureList, // 主要功能數據
      newsList, // 最新資訊數據
      goToFeature,
      backgroundStyle
    }
  }
}
</script>

<style scoped>
.q-banner {
  margin-bottom: 16px;
}

.row {
  display: flex;
  flex-wrap: wrap;
}

.col-12 {
  width: 100%;
}

.col-md-6 {
  width: 48%;
  margin-right: 4%;
}

.q-card {
  min-height: 200px;
}
</style>
