<template>
  <view class="content">
    <swiper id="swiper-list" :style="heightList[current] ? `height: ${heightList[current]}px`:''"  @change="onChange">
      <swiper-item v-for="(item,index) in list" :key="item.idx" >
        <view class="swiper-box">
          <view class="swiper-item uni-bg-red">{{item.idx}}</view>
          <image class="logo" src="/static/logo.png" v-for="i in item.idx" :key="i"></image>
        </view>
      </swiper-item>
    </swiper>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        title: 'Hello',
        list: Array.from({ length: 4 }, (_, idx) => {
          return {
            idx: idx > 2 || idx === 0 ? idx % 2 + 1 : idx
          }
        }),
        heightList:[],
        current: 0
      }
    },
    onLoad() {
      this.updateSwiper()
    },
    methods: {
      onChange(e) {
        this.current = e.detail.current
        console.log('this.current',this.current);
      },
      updateSwiper() {
       const query = uni.createSelectorQuery().in(this);
       query
         .selectAll("#swiper-list .swiper-box")
         .boundingClientRect((data) => {
           this.heightList = data.map(item=>item.height)
           // console.log("得到布局位置信息" + JSON.stringify(data));
           // console.log("节点离页面顶部的距离为" + data.top);
         })
         .exec();
      }
    }
  }
</script>

<style>
  .swiper-item {
    width: 100%;
  }
  #swiper-list  {
    height: 100%;
  }
</style>
