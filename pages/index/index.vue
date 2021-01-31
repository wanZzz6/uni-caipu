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

<style>
  .tower-swiper .tower-item {
    transform: scale(calc(0.5 + var(--index) / 10));
    margin-left: calc(var(--left) * 100upx - 150upx);
    z-index: var(--index);
  }
</style>
