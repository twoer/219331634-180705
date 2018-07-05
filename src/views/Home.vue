<template>
  <div class="home">
    <div class="header">
      <p>安徽 合肥 WEB 前端(219331634) </p>
      <p>2018/07/05 抽奖专用</p>
    </div>
    <div class="content">
      <p>{{randomMember.name || '请点击开始吧'}}</p>
    </div>
    <div class="action">
      <van-button type="primary" :block=true :loading="isStart" @click="start" >开始</van-button>
      <van-button type="danger" :block=true @click="reset">重置</van-button>
    </div>
  </div>
</template>

<script>
const MEMBER = [
  {
    name: '许瑞'
  },
  {
    name: '左强'
  },
  {
    name: '陈仁磊'
  },
  {
    name: '张坤'
  },
  {
    name: '王汉坤'
  },
  {
    name: '肖志成'
  },
  {
    name: '王晓雨'
  },
  {
    name: '三哥哥'
  },
  {
    name: '陈杰'
  },
  {
    name: '尹程'
  },
  {
    name: '李乾坤'
  },
  {
    name: '陈强'
  },
  {
    name: '尚守安'
  },
  {
    name: '单凯强'
  },
  {
    name: '邰爱强'
  },
  {
    name: '陈长裕'
  },
  {
    name: '刘东松'
  },
  {
    name: '夏彬'
  },
  {
    name: '陈文真'
  }
]
const VIP_MEMBER = [
  {
    name: '张坤'
  }
]
export default {
  name: 'home',
  data () {
    return {
      isStart: false,
      member : [],
      vipMember : [],
      luckMember : [],
      randomMember: {}
    }
  },
  created () {
    this.member = [...MEMBER]
    this.vipMember = VIP_MEMBER
  },
  methods: {
    random () {
      let _min = 0
      let _max = this.member.length - 1
      let _random = _min + Math.round(Math.random() * _max)
      return _random
    },
    start () {
      this.isStart = true
      let _count = 100
      let _interval = setInterval(()=>{
        _count --
        let _random = this.random()
        let _member = this.member[_random]
        this.randomMember = _member
        if (_count === 0) {
          clearInterval(_interval)
          this.isStart = false
          this.member.splice(_random, 1)
          this.luckMember.push(_member)
          return
        }
      }, 1000 / 20)
    },
    reset () {
      this.$dialog.confirm({
        title: '提示',
        message: '确定重置，谨慎操作？'
      }).then(() => {
        this.member = [...MEMBER]
        this.luckMember = []
        this.randomMember = {}
      }).catch(() => {
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.home
{
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding: 10px;
  .header
  {
    margin: 0px;
    line-height: 1.6em;
    font-size: 14px;
    color: #555;
    p
    {
      margin: 0px;
    }
    p:first-child
    {
      color: #444;
      font-size: 15px;
    }
  }
  .content
  {
    flex: 1;
    display: flex;
    justify-content: center;
    align-items: center;
    p
    {
      color: #333;
      font-size: 22px;
    }
  }
  .action
  {
    .van-button + .van-button
    {
      margin-top: 10px;
    }
  }
}
</style>
