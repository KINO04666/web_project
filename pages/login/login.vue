<template>
  <view class="container">
    <view class="avatar-section">
      <image class="avatar" src="/static/logo.png"></image>
    </view>
    <view class="input-section">
      <input v-model="studentId" type="text" placeholder="学号"  />
      <input v-model="password" type="password" placeholder="密码"/>
    </view>
    <button class="login-button" @click="login">登录</button>
  </view>
</template>

<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';

const studentId = ref('');
const password = ref('');
const router = useRouter();

function login() {
  if (studentId.value === '123456' && password.value === '123456') {
    uni.switchTab({
        url: '/pages/message/message'});
    
  } else {
    uni.showToast({
      title: '登录失败!',
      icon: 'none'
    });
  }
}
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100%;
}
.avatar-section {
	margin-top: 30%;
  margin-bottom: 5%;
}
.avatar {
  width: 100px;
  height: 100px;
  border-radius: 50%;
}
.input-section {
    width: 80%;
margin-bottom: 30%;
}
input {
  display: block;
  width: 100%;
  margin-bottom: 10px;
  padding: 12px; 
  box-sizing: border-box;
  border: 2px solid #ddd;
  border-radius: 15px;
  font-size: 20px;
  height: 50px;
}

.login-button {
  width: 30%;
  margin-top: 40px;
  background-color: #007AFF;
  color: white;
  border: none;
  border-radius: 5px;
}
@media (max-width: 320px) {
	.avatar-section {
		margin-top: 0%;
	  margin-bottom: 5%;
	}
  .input-section, .login-button {
    width: 90%; 
  }

  input, .login-button {
    padding: 8px; 
    font-size: 14px; 
  }
}

</style>
