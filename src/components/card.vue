<template>
<div class="card-container">
  <van-divider>Tpis</van-divider>
  <van-notice-bar
  left-icon="volume-o"
  text="输入你获得的卡密，点击提交即可兑换更新你的积分,积分是本站的虚拟货币，用于消费购买签到等功能。"
/>
<br>
<van-form @submit="onSubmit">
  <van-field
    v-model="card"
    name="card"
    label="卡密"
    placeholder="请输入卡密"
    :rules="[{ required: true, message: '请填写卡密' }]"
  />
  <div style="margin: 16px;">
    <van-button round block type="info" native-type="submit" :loading='loading'>使用</van-button>
  </div>
</van-form>
</div>
</template>

<script>
import { useKey } from '@/Interface/Recharge.js'
import { mapMutations } from 'vuex'
export default {
  name: 'card',
  data () {
    return {
      card: '',
      loading: false
    }
  },

  methods: {
    ...mapMutations(['addintegral']),
    async onSubmit ({ card }) {
      this.loading = true
      try {
        const { data: { data } } = await useKey(card)
        this.$notify({ type: 'success', message: `使用卡密成功\n积分+${data}` })
        this.addintegral(data)
        this.card = ''
      } catch (error) {
        if (error.response.status === 403) {
          this.$notify({ type: 'danger', message: '卡密错误或已被使用' })
        } else {
          this.$notify({ type: 'danger', message: '网络异常，请稍后重试..' })
        }
      }
      this.loading = false
    }
  }
}
</script>

<style lang='less' scoped>
.card-container{
.van-button--info{
background-color:#03ae84;
  border: none;
}
}

</style>
