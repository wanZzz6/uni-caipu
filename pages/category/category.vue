<template>
  <view>
    <view class="fixed">
      <cu-custom bgColor="bg-shadeTop bg-gradual-red text-white" :isBack="false">
        <block slot="backText">返回</block>
        <block slot="content">分类</block>
      </cu-custom>
    </view>

    <view class="VerticalBox">
      <!-- 左侧 -->
      <scroll-view class="VerticalNav nav" scroll-y scroll-with-animation :scroll-top="verticalNavTop" style="height:100vh;padding-top: 220upx;">
        <view class="cu-item" :class="index==tabCur?'text-green cur':''" v-for="(item,index) in list" :key="index" @tap="TabSelect"
          :data-id="index">
          {{item.name}}
        </view>
      </scroll-view>

      <!-- 右侧 -->
      <scroll-view class="VerticalMain padding-top" scroll-y scroll-with-animation style="height:100vh;padding-top: 200upx;"
        :scroll-into-view="'main-'+mainCur" @scroll="VerticalMain">
        <view class="padding-top padding-lr" v-for="(item,index) in list" :key="index" :id="'main-'+index">
          <view class="cu-bar solid-bottom bg-white">
            <view class="action">
              <text class="cuIcon-title text-green"></text> {{item.name}}</view>
          </view>
          <view class="cu-list menu-avatar">
            <view class="cu-item">
              <view class="row">
                <view class="col-8" v-for="(item, index) in 9" :key="index">
                  菜谱-{{index}}
                </view>
              </view>
            </view>

          </view>
        </view>
      </scroll-view>
    </view>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        list: [],
        tabCur: 0,
        mainCur: 0,
        verticalNavTop: 0,
        load: true
      };
    },
    onLoad() {
      uni.showLoading({
        title: '加载中...',
        mask: true
      });
      let list = [{
          id: 1,
          name: '家常菜谱'
        },
        {
          id: 2,
          name: '国内菜谱'
        },
        {
          id: 3,
          name: '国外菜谱'
        },
      ];
      // for (let i = 0; i < 26; i++) {
      // 	list[i] = {};
      // 	list[i].name = String.fromCharCode(65 + i);
      // 	list[i].id = i;
      // }
      this.list = list;
      this.listCur = list[0];
    },
    onReady() {
      uni.hideLoading()
    },
    methods: {
      TabSelect(e) {
        this.tabCur = e.currentTarget.dataset.id;
        this.mainCur = e.currentTarget.dataset.id;
        this.verticalNavTop = (e.currentTarget.dataset.id - 1) * 50
      },
      VerticalMain(e) {
        // #ifdef MP-ALIPAY
        return false //支付宝小程序暂时不支持双向联动 
        // #endif
        let that = this;
        let tabHeight = 0;
        if (this.load) {
          for (let i = 0; i < this.list.length; i++) {
            let view = uni.createSelectorQuery().select("#main-" + this.list[i].id);
            view.fields({
              size: true
            }, data => {
              this.list[i].top = tabHeight;
              tabHeight = tabHeight + data.height;
              this.list[i].bottom = tabHeight;
            }).exec();
          }
          this.load = false
        }
        let scrollTop = e.detail.scrollTop + 10;
        for (let i = 0; i < this.list.length; i++) {
          if (scrollTop > this.list[i].top && scrollTop < this.list[i].bottom) {
            this.verticalNavTop = (this.list[i].id - 1) * 50
            this.tabCur = this.list[i].id
            console.log(scrollTop)
            return false
          }
        }
      }
    },
  }
</script>

<style lang="less">
  .fixed {
    position: fixed;
    z-index: 99;
  }

  .VerticalNav.nav {
    width: 200upx;
    padding-top: 150upx;
    background-color: white;
    white-space: initial;
  }

  .VerticalNav.nav .cu-item {
    width: 100%;
    text-align: center;
    background-color: #fff;
    margin: 0;
    border: none;
    height: 50px;
    position: relative;
  }

  .VerticalNav.nav .cu-item.cur {
    background-color: #f1f1f1;
  }

  .VerticalNav.nav .cu-item.cur::after {
    content: "";
    width: 8upx;
    height: 30upx;
    border-radius: 10upx 0 0 10upx;
    position: absolute;
    background-color: currentColor;
    top: 0;
    right: 0upx;
    bottom: 0;
    margin: auto;
  }

  .VerticalBox {
    display: flex;
  }

  .VerticalMain {
    background-color: #f1f1f1;
    flex: 1;
  }

  .VerticalMain .cu-list.menu-avatar>.cu-item {
    height: auto;
  }

  .cu-list {
    overflow: hidden;
  }


  .cu-item {
    padding: 20upx 0;

    .row {
      text-align: center;

      &>view {
        padding: 10upx 20upx;
        margin: 10upx;
      }
    }


  }
</style>
