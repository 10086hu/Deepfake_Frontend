<template>
  <div class="news-detection">
    <h2>新闻检测</h2>

    <div class="input-section">
      <div class="upload-area">
        <label class="upload-label" @click="triggerImageUpload">
          <img v-if="imageUrl" :src="imageUrl" alt="上传图片" class="preview-img" />
          <div v-else class="upload-placeholder">点击上传图片</div>
          <input type="file" ref="fileInput" accept="image/*" @change="handleImageUpload" style="display: none;" />
        </label>
      </div>

      <div class="text-area">
        <textarea v-model="textInput" placeholder="请输入新闻文字内容..."></textarea>
      </div>
    </div>

    <button @click="handleDetection">检测</button>
    <div class="message" v-if="message">{{ message }}</div>

    <div class="output-section" v-if="resultImage">
      <h3>检测结果</h3>
      <img :src="resultImage" alt="检测结果" class="result-img" />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const imageUrl = ref('')
const textInput = ref('')
const message = ref('')
const resultImage = ref('')
const fileInput = ref(null)

const triggerImageUpload = () => {
  fileInput.value.click()
}

const handleImageUpload = (e) => {
  const file = e.target.files[0]
  if (file) {
    const reader = new FileReader()
    reader.onload = () => {
      imageUrl.value = reader.result
    }
    reader.readAsDataURL(file)
  }
}

const handleDetection = () => {
  if (!imageUrl.value && !textInput.value.trim()) {
    message.value = '请上传图片或输入文字内容'
    return
  }

  message.value = ''
  
  // 模拟检测逻辑，这里可以替换为调用后端 API
  setTimeout(() => {
    resultImage.value = imageUrl.value || 'https://via.placeholder.com/400x300?text=处理结果'
  }, 1000)
}
</script>

<style scoped>
.news-detection {
  padding: 20px;
}

.input-section {
  display: flex;
  gap: 2rem;
  margin-bottom: 1rem;
}

.upload-area {
  flex: 1;
}

.upload-label {
  display: block;
  border: 2px dashed #ccc;
  padding: 1rem;
  text-align: center;
  cursor: pointer;
  border-radius: 6px;
}

.upload-placeholder {
  color: #aaa;
  font-size: 14px;
}

.preview-img {
  max-width: 100%;
  max-height: 200px;
  object-fit: contain;
}

.text-area {
  flex: 2;
}

textarea {
  width: 100%;
  height: 150px;
  padding: 0.5rem;
  resize: none;
  border: 1px solid #ccc;
  border-radius: 6px;
}

button {
  padding: 0.5rem 1rem;
  background-color: #409eff;
  color: white;
  border: none;
  border-radius: 6px;
  cursor: pointer;
}

button:hover {
  background-color: #307ec7;
}

.message {
  color: red;
  margin-top: 0.5rem;
}

.output-section {
  margin-top: 2rem;
}

.result-img {
  max-width: 100%;
  border: 1px solid #ccc;
  border-radius: 6px;
}
</style>
