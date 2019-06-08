<template>
  <div>
    <swiper :indicator-dots="opts.indicatorDots"
            :autoplay="opts.autoplay" :interval="opts.interval" :duration="opts.duration">
      <block v-for="item in swiper.nodeList" :key="item.prdpackId">
        <swiper-item>
          <img :src="'http://www.miguvideo.com'+item.imageSrcH" class="slide-image"/>
        </swiper-item>
      </block>
    </swiper>
    <div>
      <p class="title">{{hots.nodeName}}</p>
      <block v-for="item in hots.nodeList" :key="item.prdpackId">
        <div class="item">
          <img class="item-img" :src="'http://www.miguvideo.com'+item.imageSrcH" alt="">
          <div class="item-info">
            <p class="name">{{item.name}}</p>
            <p class="detail">{{item.detail}}</p>
            <p class="updatecycle">{{item.updatecycle}} <span>{{item.score}}</span></p>
          </div>
        </div>
      </block>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        opts: {
          indicatorDots: true,
          autoplay: true,
          interval: 3000,
          duration: 500
        },
        swiper: {},
        hots: {}
      }
    },

    methods: {
      _initData() {
        this.showLoading()
        let that = this
        let url = 'http://www.miguvideo.com/wap/resource/pc/data/channelData.jsp?nodeId=70027519&pagesize=3&pageidx=1';
        wx.request({
          type: 'get',
          url,
          success(res) {
            that.swiper = res.data[0]
            that.hots = res.data[1]
            that.closeLoading()
          }
        })
      },
      showLoading() {
        wx.showLoading({
          title: '加载中...',
        })
      },
      closeLoading() {
        wx.hideLoading()
      }
    },

    created() {
      this._initData()
    }
  }
</script>

<style scoped>
  .slide-image {
    width: 100%;
    height: 360 rpx;
  }
  .title{
    line-height: 48rpx;
    font-size: 48rpx;
    margin: 24rpx;
    border-left: 4rpx solid #87CEEB;
    color: #87CEEB;
    padding-left: 24rpx;
  }
  .item{
    display: flex;
    padding: 24rpx;
    margin-top: 12rpx;
    background-color: #fff;
  }
  .item-img{
    width: 240rpx;
    height: 240rpx;
    margin-right: 12rpx;
  }
  .item-info{
    flex: 1;
    font-size: 24rpx;
  }
  .name{
    font-size: 32rpx;
  }
  .detail{
    margin-top: 16rpx;
    height: 124rpx;
    overflow: hidden;
    margin-bottom: 24rpx;
  }
</style>
