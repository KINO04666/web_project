<template>
  <view class="chat-container">
    <!-- 顶部标题栏显示聊天对象名称 -->
    <view class="chat-header">{{ chatName }}</view>
    <!-- 消息列表区 -->
    <view class="message-list">
      <view v-for="(message, index) in messages" :key="index" :class="{'my-message': message.isMine, 'other-message': !message.isMine}">
        <image :src="message.avatar" class="avatar" />
        <view class="message-content">
          <text class="message-text">{{ message.text }}</text>
        </view>
      </view>
    </view>
    <!-- 输入和发送按钮区 -->
    <view class="input-area">
      <input v-model="newMessage" type="text" placeholder="输入消息..." class="input-field"/>
      <button @click="sendMessage" class="send-button">发送</button>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      chatName: '',  // 从路由参数获取聊天对象名称
      newMessage: '',
      messages: [
        { text: '你晚上要回来吃饭吗？', isMine: false, avatar: '/static/cherry_pic.png' },
        { text: '我不回来了，有事外面吃。', isMine: true, avatar: '/static/cherry_pic.png' }
      ]
    };
  },
  methods: {
    sendMessage() {
      if (this.newMessage.trim() !== '') {
        this.messages.push({
          text: this.newMessage,
          isMine: true,
          avatar: '/static/cherry_pic.png' // 修改为用户自己的头像
        });
        this.newMessage = '';
      }
    }
  },
  onLoad(options) {
      // 确保这里使用的方法名和你的实际框架版本匹配
      this.chatName = options.name || '未知联系人'; // 从路由参数中获取聊天对象名称
    },
}
</script>

<style scoped>
.chat-container {
  display: flex;
  flex-direction: column;
  height: 100%;
}
.chat-header {
  padding: 10px;
  font-size: 18px;
  text-align: center;
  background-color: #f3f3f3;
}
.message-list {
  flex: 1;
  overflow-y: scroll;
  padding: 10px;
}
.my-message, .other-message {
  display: flex;
  margin-bottom: 10px;
}
.my-message {
  justify-content: flex-end;
}
.other-message {
  justify-content: flex-start;
}
.avatar {
  width: 40px;
  height: 40px;
  border-radius: 20px;
}
.message-content {
  max-width: 70%;
  background-color: #f0f0f0;
  padding: 8px;
  border-radius: 10px;
  margin: 5px;
}
.input-area {
  display: flex;
  padding: 10px;
  background-color: #fff;
  border-top: 1px solid #ccc;
  position: fixed; /* 新增固定位置属性 */
  bottom: 0; /* 设置为屏幕底部 */
  left: 0; /* 从左边界开始 */
  right: 0; /* 延伸到右边界 */
  box-sizing: border-box; /* 确保padding不会影响宽度计算 */
}

.input-field {
  flex: 1;
  margin-right: 10px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  height: 40px; /* 调整高度 */
}

.send-button {
  padding: 10px 20px;
  background-color: #007aff;
  color: white;
  border: none;
  border-radius: 4px;
  height: 60px; /* 确保和输入框高度一致 */
}
</style>
