<template>
 <div class="home-container">
<van-nav-bar :left-text='toDay' right-text='•••' />
<van-notice-bar color="#1989fa" background="#ecf9ff" left-icon="info-o">
本站自动签到程序采用分布式运行.安全稳定快速。
</van-notice-bar>
<p class="text-p">本网站使用步骤：</p>
<van-steps direction="vertical" :active="active">
  <van-step v-for="(item,index) in explainList" :key="item">
    <h3 @click="updateActive(index)">{{item}}</h3>
  </van-step>
</van-steps>
<p class="text">
邀请人免费得2积分，也就是一个月自动签到权限。<br>
不想邀请人也可以选择钞能力，2块钱10积分 ：<a href="https://www.126sh.com/details/77801D34" target="_blank"> 购买卡密地址</a><br>
本站技术栈(springboot+vue)，源码包搭建包更新联系qq3403106098</p>
  </div>
</template>

<script>
import { mapState } from 'vuex'
export default {
  name: 'Home',
  data () {
    return {
      active: 2,
      explainList: ['使用卡密兑换积分', '使用积分兑换签到功能', '设置每门课程签到']
    }
  },
  computed: {
    ...mapState(['user']),
    toDay () {
      const Now = new Date()
      const Hour = Now.getHours()
      if (Hour < 6) { return `凌晨好！${this.user.userInfo.username}` } else if (Hour < 9) { return `早上好！${this.user.userInfo.username}` } else if (Hour < 12) { return `上午好！${this.user.userInfo.username}` } else if (Hour < 14) { return `中午好！${this.user.userInfo.username}` } else if (Hour < 17) { return `下午好！${this.user.userInfo.username}` } else if (Hour < 19) { return `傍晚好！${this.user.userInfo.username}` } else if (Hour < 22) { return `晚上好！${this.user.userInfo.username}` } else { return `夜里好！${this.user.userInfo.username}` }
    }
  },
  methods: {
    updateActive (index) {
      this.active = index
    }
  }
}
</script>

<style lang='less' scoped>
.home-container{
  .text-p{
    padding-left: 40px;
  }
  .text{
    font-size: 30px;
    padding: 20px;
  }
  .van-nav-bar{
    background: #03ae84;
 /deep/   .van-nav-bar__text{
      color: white;
    }
  }
}
</style>
