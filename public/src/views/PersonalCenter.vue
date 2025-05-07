<template>
  <div class="personal-center">
    <h2>个人中心</h2>

    <div class="profile">
      <div class="avatar-wrapper" @click="triggerAvatarSelect">
        <img :src="avatarUrl" alt="头像" class="avatar" />
      </div>
      <input type="file" ref="fileInput" @change="handleAvatarChange" accept="image/*" style="display: none;" />
    </div>

    <div class="info">
      <label>用户名：</label>
      <input v-model="editableUsername" />
    </div>

    <div class="info">
      <label>邮箱：</label>
      <input :value="email" disabled />
    </div>

    <button @click="saveChanges">保存修改</button>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const username = ref('张三')
const email = ref('zhangsan@example.com')
const avatarUrl = ref('https://via.placeholder.com/100')

const editableUsername = ref(username.value)
const fileInput = ref(null)

const triggerAvatarSelect = () => {
  fileInput.value.click()
}

const handleAvatarChange = (e) => {
  const file = e.target.files[0]
  if (file) {
    const reader = new FileReader()
    reader.onload = () => {
      avatarUrl.value = reader.result
    }
    reader.readAsDataURL(file)
  }
}

const saveChanges = () => {
  username.value = editableUsername.value
  alert('修改已保存（模拟）')
}
</script>

<style scoped>
.personal-center {
  padding: 20px;
  max-width: 500px;
}

.profile {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 1rem;
}

.avatar-wrapper {
  cursor: pointer;
  border-radius: 50%;
  overflow: hidden;
  border: 2px solid #409eff;
  width: 100px;
  height: 100px;
  display: inline-block;
}

.avatar {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.info {
  margin-bottom: 1rem;
}

label {
  display: inline-block;
  width: 70px;
}

input[type="text"] {
  width: 100%;
  padding: 0.5rem;
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
</style>
