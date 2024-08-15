<script setup>
import { ref } from 'vue'
import CountTime from "./CountTime.vue";

defineProps({
  msg: String,
})

const phoneNumber = ref('123-456-7890');
const verificationCode = ref('ABC123');



const copyToClipboard = (text) => {
  navigator.clipboard.writeText(text).then(() => {
    alert('已复制！');
  }).catch(err => {
    console.error('复制失败:', err);
  });
};

const showModal = ref(true);
</script>

<template>
  <h1>{{ msg }}</h1>
  <div>
    <div class="box" style="background: #33B953">
      <h2>醒图vip</h2>
      <div class="card-body">
        <p>手机号获取中</p>
      </div>
      <div>
        <button @click="copyToClipboard(phoneNumber)">复制手机号</button>
      </div>
    </div>


    <div class="box" style="background: #E9CD08">
      <h2>验证码</h2>
      <div class="card-body">
        <p>等待验证码....</p>
        <CountTime :initialTime="30" /> <!-- 300秒（5分钟）的倒计时 -->
        <h5 style="color: #ff0000">（倒计时结束验证码没显示请联系淘宝客服）</h5>
        <h5 style="color: #ff0000">（显示数字验证码之后再点复制验证码）</h5>
      </div>
      <div class="right">
        <button @click="copyToClipboard(verificationCode)">复制验证码</button>
      </div>
    </div>

    <div class="box" style="background-color: #007bff">
      <h2>教程</h2>
      <div class="card-body " >
        <div class="jc">
          <h3>①&nbsp;.&nbsp;复制手机号到醒图软件登录</h3>
          <h3>②&nbsp;.&nbsp;醒图软件内输入复制的手机号登录</h3>
          <h3>③&nbsp;.&nbsp;返回此页面查看验证码信息</h3>
          <h3>④&nbsp;.&nbsp;复制验证码信息输入到醒图软件内</h3>
          <h3>⑤&nbsp;.&nbsp;醒图APP内请勿多次获取验证码</h3>
          <h3>⑥&nbsp;.&nbsp;遇到问题请联系淘宝客服</h3>
        </div>
      </div>
    </div>

    <div class="modal-overlay" v-if="showModal">
      <div class="modal-content">
        <button class="close-button" @click.self="showModal = false">&times;</button>
        <img src="../assets/tp.png" alt="Modal Image" />
      </div>
    </div>
  </div>
</template>

<style scoped>

.box{
  color: white;
  padding: 1rem 0;
  margin: 2rem 0;
  border-radius: 1em;
}
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background: #fff;
  padding: 20px;
  position: relative;
}

.modal-content img {
  max-width: 100%;
  height: auto;
}

.close-button {
  position: absolute;
  top: 10px;
  right: 10px;
  background: none;
  border: none;
  font-size: 24px;
  cursor: pointer;
  color: #333;
}
</style>
