<template>
  <view class="chat-container">
    <!-- 顶部标题栏显示聊天对象名称 -->
    <view class="chat-header">{{ chatName }}
	      <view class="back-button" @click="goBack">&#9664; 返回</view>
	</view>
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
    },
	  goBack() {
	    // 实现返回上一页的功能
	    uni.navigateBack({
	      delta: 1 // 返回上一级页面
	    });
	  }
  },
  onLoad(options) {
    // 使用decodeURIComponent解码接收到的名称
    this.chatName = decodeURIComponent(options.name || '未知联系人');
  }
}
</script>

<style scoped>
.back-button {
  position: absolute;
  left: 10px; /* 设置左侧的具体位置 */
  top: 10px; /* 根据需要调整垂直位置 */
  font-size: 16px;
  cursor: pointer;
}
.chat-container {
  display: flex;
  flex-direction: column;
  height: 100%;
}
.chat-header {
  display: flex;
  align-items: center;
  justify-content: center; /* 确保整体内容居中 */
  position: relative; /* 为绝对定位的返回按钮设置相对定位的参考 */
  padding: 10px;
  font-size: 18px;
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
