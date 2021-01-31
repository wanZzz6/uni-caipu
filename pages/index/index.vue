<template>
  <view class="content">
    <cu-custom bgColor="bg-gradual-red" :isBack="false">
      <block slot="backText">返回</block>
      <block slot="content">首页</block>
    </cu-custom>

    <!-- 轮播图 -->
    <swiper class="screen-swiper" :class="dotStyle?'square-dot':'round-dot'" :indicator-dots="true" :circular="true"
      :autoplay="true" interval="5000" duration="500">
      <swiper-item v-for="(item,index) in swiperList" :key="index">
        <image :src="item.url" mode="aspectFill" v-if="item.type=='image'"></image>
        <video :src="item.url" autoplay loop muted :show-play-btn="false" :controls="false" objectFit="cover" v-if="item.type=='video'"></video>
      </swiper-item>
    </swiper>

    <view class="tools row bg-white">
      <view class="col-8">
        <image src="../../static/tools/navbg0.png" mode="widthFix"></image>
        <text>最热菜谱</text>
      </view>
      <view class="col-8">
        <image src="../../static/tools/navbg1.png" mode="widthFix"></image>
        <text>最热菜谱</text>
      </view>
      <view class="col-8">
        <image src="../../static/tools/navbg2.png" mode="widthFix "></image>
        <text>美食专题</text>
      </view>
      <view class="col-8">
        <image src="../../static/tools/navbg3.png" mode="widthFix "></image>
        <text>家常菜谱</text>
      </view>
      <view class="col-8">
        <image src="../../static/tools/navbg4.png" mode="widthFix "></image>
        <text>中国菜谱</text>
      </view>
      <view class="col-8">
        <image src="../../static/tools/navbg5.png" mode="widthFix "></image>
        <text>外国菜谱</text>
      </view>
    </view>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        swiperList: [{
          id: 0,
          type: 'image',
          url: 'https://ossweb-img.qq.com/images/lol/web201310/skin/big84000.jpg'
        }, {
          id: 1,
          type: 'image',
          url: 'https://ossweb-img.qq.com/images/lol/web201310/skin/big37006.jpg',
        }, {
          id: 2,
          type: 'image',
          url: 'https://ossweb-img.qq.com/images/lol/web201310/skin/big39000.jpg'
        }, {
          id: 3,
          type: 'image',
          url: 'https://ossweb-img.qq.com/images/lol/web201310/skin/big10001.jpg'
        }],
        dotStyle: true,
      };
    },
    onLoad() {},
    methods: {}
  }
</script>

<style lang="less">
  .tower-swiper .tower-item {
    transform: scale(calc(0.5 + var(--index) / 10));
    margin-left: calc(var(--left) * 100upx - 150upx);
    z-index: var(--index);
  }

  .content {}

  .tools {
    &>view {
      text-align: center;
      overflow: hidden;
      padding: 10upx 8%;

      image {
        width: 100upx;
        height: 100upx;
      }

      text {
        display: block;
        font-size: 14px;
        color: #1CBBB4;
      }
    }

  }
</style>
