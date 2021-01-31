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

    <!-- 标题 -->
    <view class="cu-bar bg-white margin-top">
      <view class="action">
        <text class="cuIcon-title text-green"></text>
        <text class="text-xl text-bold">最热推荐</text>
      </view>
    </view>
    <!-- 列表 -->
    <view class="list row bg-white" style="">
      <view class="col-8">
        <image class="solid" src="http://pic.soucaipu.cn/allimg/c191230/15MC1234A560-15Q4.jpg" mode="widthFix"></image>
        <text class="margin-top-xs">最热菜谱</text>
      </view>
      <view class="col-8">
        <image class="solid" src="http://pic.soucaipu.cn/allimg/c200211/15Q40942IB20-63N7.jpg" mode="widthFix"></image>
        <text class="margin-top-xs">酱汁烤五花肉</text>
      </view>
      <view class="col-8">
        <image class="solid" src="http://pic.soucaipu.cn/allimg/c191230/15MBF5122130-12539.jpg" mode="widthFix"></image>
        <text class="margin-top-xs">韩式酸辣炒饭</text>
      </view>
      <view class="col-8">
        <image class="solid" src="http://pic.soucaipu.cn/allimg/c200211/15Q406251bP-43A6.jpg" mode="widthFix"></image>
        <text class="margin-top-xs">玫瑰糟汁五花肉</text>
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
        width: 80upx;
        height: 80upx;
      }

      text {
        display: block;
        font-size: 14px;
        color: #1CBBB4;
      }
    }
  }

  .list {
    &>view {
      text-align: center;
      overflow: hidden;
      padding: 3% 4%;
      margin-bottom: 15upx;

      // &:first-child{
      //   padding-left: 6%;
      // }
      // &:last-child{
      //   padding-right: 6%;
      // }

      image {
        width: 190upx;
        // height: 80upx;
      }

      text {
        display: block;
        font-size: 14px;
        color: #1CBBB4;
      }
    }
  }
</style>
