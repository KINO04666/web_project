<template>
  <view class="container">
    <view class="chat-item" v-for="(chat, index) in chats" :key="index" @click="openChat(chat)">
      <image :src="chat.avatar" class="avatar" />
      <view class="chat-info">
        <text class="name">{{ chat.name }}</text>
        <text class="last-message">{{ chat.lastMessage }}</text>
      </view>
      <text class="time">{{ chat.time }}</text>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      chats: [
        {
          name: '姐姐',
          avatar: '/static/cherry_pic.png',
          lastMessage: '你晚上要回来吃饭吗？',
          time: '18:45'
        },
        {
          name: 'Tom',
          avatar: '/static/cherry_pic.png',
          lastMessage: '项目的最新文件我已经发你了。',
          time: '17:30'
        },
        {
          name: 'Alice',
          avatar: '/static/cherry_pic.png',
          lastMessage: '周末去爬山吗？',
          time: '08:20'
        },
        // 更多聊天记录
      ]
    };
  },
  methods: {
    openChat(chat) {
      console.log(`Opening chat with ${chat.name}`);
      // 这里应该有页面跳转逻辑，示例只做打印处理
       uni.navigateTo({
        url: `/pages/chat/chat?name=${encodeURIComponent(chat.name)}`       });
    }
  }
}
</script>

<style>
.container {
  padding: 10px;
}
.chat-item {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
  cursor: pointer;
}
.avatar {
  width: 50px;
  height: 50px;
  border-radius: 25px;
  margin-right: 10px;
}
.chat-info {
  flex: 1;
}
.name {
  font-weight: bold;
  font-size: 16px;
}
.last-message {
  color: #666;
  font-size: 14px;
}
.time {
  color: #999;
  font-size: 12px;
}
</style>
