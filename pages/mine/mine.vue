<template>
  <view class="container">
    <view class="profile-section">
      <image class="avatar" src="/static/cherry_pic.png" />
      <view class="editable-info">
        <view class="info-row">
          <text class="label">姓名：</text>
          <input v-model="profile.name" class="input" />
        </view>
        <view class="info-row">
          <text class="label">用户名：</text>
          <input v-model="profile.username" class="input" />
        </view>
        <view class="info-row">
          <text class="label">学号：</text>
          <text class="fixed-info">{{ profile.studentId }}</text>
        </view>
      </view>
      <button @click="saveProfile">保存</button>
    </view>
    <view class="posts">
          <view class="post" v-for="(post, index) in posts" :key="index">
            <image :src="post.image" class="post-image"/>
            <text class="post-text">{{ post.text }}</text>
            <text class="post-date">{{ post.date }}</text>
          </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      profile: {
        name: '张三',
        username: 'zhangsan123',
        studentId: '20230001'
      },
	    posts: [
	          { image: '/static/mh.jpg', text: '今天的花真美！', date: '2023-05-07' },
	          { image: '/static/bg2.jpg', text: '刚刚看到的风景！', date: '2023-05-06' }
	    ]
      // 图文内容数据未更改
    };
  },
  methods: {
    saveProfile() {
      // 保存个人信息的逻辑，可能包括调用API等
      console.log('保存个人信息', this.profile);
    }
  }
}
</script>

<style>
.container {
  padding: 20px;
}
.profile-section {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 20px;
}
.avatar {
  width: 80px;
  height: 80px;
  border-radius: 40px;
  margin-bottom: 20px;
}
.editable-info {
  width: 100%;
}
.info-row {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}
.label {
  width: 80px; /* Label宽度 */
  font-size: 16px;
}
.input {
  flex: 1;
  height: 32px;
  padding: 0 10px;
  font-size: 16px;
  border: 1px solid #ccc;
}
.fixed-info {
  font-size: 16px;
  color: #333;
}
.posts {
  display: flex;
  flex-direction: column;
}
/* 其他样式保持不变 */
</style>
