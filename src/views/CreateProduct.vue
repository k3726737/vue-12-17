<template>
  <q-page padding>
    <!-- 產品表單卡片 -->
    <q-card>
      <!-- 標題 -->
      <q-card-section>
        <div class="text-h6">產品表單</div>
        <div class="text-subtitle2">請輸入產品資訊</div>
      </q-card-section>

      <!-- 表單內容 -->
      <q-card-section>
        <q-form ref="formRef" @submit="submitForm" @reset="resetForm">
          <!-- 使用 v-for 產生表單欄位 -->
          <div v-for="(field, index) in formFields" :key="index" class="q-mb-md">
            <!-- q-input -->
            <q-input
              v-if="field.type === 'input'"
              v-model="formData[field.model]"
              :label="field.label"
              :type="field.inputType || 'text'"
              :rules="field.rules"
              outlined
              dense
              clearable
            />

            <!-- q-select -->
            <q-select
              v-else-if="field.type === 'select'"
              v-model="formData[field.model]"
              :label="field.label"
              :options="field.options"
              :rules="field.rules"
              outlined
              dense
              emit-value
              map-options
            />

            <!-- q-checkbox -->
            <q-checkbox
              v-else-if="field.type === 'checkbox'"
              v-model="formData[field.model]"
              :label="field.label"
            />
          </div>

          <!-- 按鈕區塊 -->
          <div class="q-mt-md">
            <q-btn
              label="提交"
              color="primary"
              type="submit"
              class="full-width"
            />
            <q-btn
              label="重置"
              type="reset"
              color="secondary"
              flat
              class="full-width q-mt-sm"
            />
          </div>
        </q-form>
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script>
import { ref } from 'vue'
import { useQuasar } from 'quasar'
import * as yup from 'yup'

export default {
  setup () {
    const $q = useQuasar()

    // 表單數據
    const formData = ref({
      name: '',
      price: null,
      description: '',
      category: null,
      inStock: false
    })

    // 表單欄位設定
    const formFields = ref([
      {
        label: '產品名稱',
        model: 'name',
        type: 'input',
        rules: [val => !!val || '此為必填項']
      },
      {
        label: '價格 (NTD)',
        model: 'price',
        type: 'input',
        inputType: 'number',
        rules: [
          val => !!val || '此為必填項',
          val => val > 0 || '價格必須大於零'
        ]
      },
      {
        label: '產品描述',
        model: 'description',
        type: 'input',
        inputType: 'textarea',
        rules: [val => !!val || '此為必填項']
      },
      {
        label: '類別',
        model: 'category',
        type: 'select',
        options: [
          { label: '電子產品', value: 'electronics' },
          { label: '服飾', value: 'apparel' },
          { label: '家居用品', value: 'home' },
          { label: '書籍', value: 'books' },
          { label: '戒指', value: 'ring' },
          { label: '手鍊', value: 'bracelet' },
          { label: '耳環', value: 'earrings' },
          { label: '項鍊', value: 'necklace' }
        ],
        rules: [val => !!val || '請選擇產品類別']
      },
      {
        label: '有庫存',
        model: 'inStock',
        type: 'checkbox'
      }
    ])

    // Yup 驗證規則
    const schema = yup.object({
      name: yup.string().required('產品名稱為必填項'),
      price: yup
        .number()
        .typeError('價格必須是數字')
        .positive('價格必須大於零')
        .required('價格為必填項'),
      description: yup.string().required('產品描述為必填項'),
      category: yup.string().required('請選擇產品類別'),
      inStock: yup.boolean()
    })

    // 提交表單
    const submitForm = async () => {
      try {
        await schema.validate(formData.value, { abortEarly: false })
        $q.notify({ type: 'positive', message: '產品資訊已成功提交！' })
        console.log('表單數據:', formData.value) // 模擬提交
      } catch (err) {
        const errors = err.inner.map(e => e.message)
        errors.forEach(error => {
          $q.notify({ type: 'negative', message: error })
        })
      }
    }

    // 重置表單
    const resetForm = () => {
      formData.value = {
        name: '',
        price: null,
        description: '',
        category: null,
        inStock: false
      }
      $q.notify({ type: 'info', message: '表單已重置' })
    }

    return { formData, formFields, submitForm, resetForm }
  }
}
</script>

<style scoped>
.full-width {
  width: 100%;
}
.q-mb-md {
  margin-bottom: 16px;
}
</style>
