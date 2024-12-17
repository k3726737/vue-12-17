<template>
  <q-page padding>
    <!-- 標題工具欄 -->
    <q-toolbar>
      <q-toolbar-title>用戶資訊</q-toolbar-title>
      <q-btn label="編輯" color="primary" @click="editMode = !editMode" />
    </q-toolbar>

    <!-- 用戶資訊卡片 -->
    <q-card
      class="q-mb-md"
      v-for="(user, index) in users"
      :key="index"
    >
      <q-card-section>
        <div class="text-h6 q-mb-md">測試人員</div>
        <q-separator class="q-mb-md" />

        <!-- 用戶姓名 -->
        <q-input
          v-model="user.name"
          label="姓名"
          :disabled="!editMode"
          outlined
          dense
          class="q-mb-md"
        />

        <!-- 用戶電子郵件 -->
        <q-input
          v-model="user.email"
          label="電子郵件"
          :disabled="!editMode"
          outlined
          dense
          class="q-mb-md"
        />

        <!-- 用戶角色 -->
        <q-select
          v-model="user.role"
          label="角色"
          :options="roles"
          :disable="!editMode"
          outlined
          dense
          class="q-mb-md"
        />

        <!-- 註冊日期 -->
        <q-input
          v-model="user.registrationDate"
          label="註冊日期"
          :disabled="true"
          outlined
          dense
          class="q-mb-md"
        />
      </q-card-section>

      <!-- 保存與取消按鈕 -->
      <q-card-actions align="right" class="q-mt-sm">
        <q-btn
          label="取消"
          color="negative"
          flat
          @click="cancelEdit(index)"
          v-if="editMode"
        />
        <q-btn
          label="保存"
          color="positive"
          flat
          @click="saveUserInfo(index)"
          v-if="editMode"
        />
      </q-card-actions>
    </q-card>
  </q-page>
</template>

<script>
import { ref } from 'vue'

export default {
  setup () {
    // 用戶資料（多位用戶）
    const users = ref([
      {
        name: '王小明',
        email: 'xiaoming@example.com',
        role: '會員',
        registrationDate: '2023-05-01'
      },
      {
        name: '李光湖',
        email: 'lisicho@example.com',
        role: '管理員',
        registrationDate: '2023-06-15'
      },
      {
        name: '張小強',
        email: 'zhangsan@example.com',
        role: '來賓',
        registrationDate: '2023-07-20'
      }
    ])

    // 角色選項
    const roles = ref(['會員', '管理員', '來賓'])

    // 編輯模式開關
    const editMode = ref(false)

    // 保存用戶資訊
    const saveUserInfo = (index) => {
      console.log(`保存用戶 ${users.value[index].name} 資訊`, users.value[index])
      editMode.value = false
    }

    // 取消編輯
    const cancelEdit = (index) => {
      users.value[index] = {
        name: index === 0 ? '王小明' : index === 1 ? '李四' : '張三',
        email: index === 0 ? 'xiaoming@example.com' : index === 1 ? 'lisi@example.com' : 'zhangsan@example.com',
        role: index === 0 ? '會員' : index === 1 ? '管理員' : '來賓',
        registrationDate: index === 0 ? '2023-05-01' : index === 1 ? '2023-06-15' : '2023-07-20'
      }
      editMode.value = false
    }

    return {
      users,
      roles,
      editMode,
      saveUserInfo,
      cancelEdit
    }
  }
}
</script>

<style scoped>
.q-card {
  max-width: 600px;
  margin: 0 auto;
}
</style>
