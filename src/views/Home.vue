<template>
  <div class="home">
    <div class="header">
      <p>合肥 PHP & FE  聚餐</p>
      <p>2018/08/11 抽奖专用</p>
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
  {name: '夏彬'},
  {name: '高进'},
  {name: '王菁菁'},
  {name: '左强'},
  {name: '张涛'},
  {name: '郑家园'},
  {name: '陈志远'},
  {name: '张海洲'},
  {name: '安明兴'},
  {name: '高大成'},
  {name: '许伟'},
  {name: '赵明亮'},
  {name: '陈强'},
  {name: '林泳波'},
  {name: '郑旭'},
  {name: '李勇'},
  {name: '张坤'},
  {name: '沈强'},
  {name: '王晓雨'},
  {name: '沈美玉'},
  {name: '常弘扬'},
  {name: '李辰辰'},
  {name: '杨斌'},
  {name: '洪涛'},
  {name: '吴礼恺'},
  {name: '杨安娜'},
  {name: '胡园园'},
  {name: '胡萍萍'},
  {name: '葛磊'},
  {name: '张亮亮'},
  {name: '孔海涛'},
  {name: '吴建峰'},
  {name: '章玲'},
  {name: '姜言言'},
  {name: '胡文'},
  {name: '贾宝川'},
  {name: '沈财'},
  {name: '潘德政'}
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
