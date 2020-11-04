<template>
  <view>
    <view>
      <image
        src="../../static/tabbar/1.jpg"
        class="img"
        style="width: 750rpx; height: 300rpx"
      ></image>
    </view>
    <!--轮播图-->
    <swiper
      :indicator-dots="true"
      :autoplay="true"
      :interval="3000"
      :duration="200"
      style="width: 750rpx; height: 250rpx"
    >
      <swiper-item>
        <image
          src="../../static/tabbar/1.jpg"
          style="width: 750rpx; height: 250rpx"
        ></image>
      </swiper-item>

      <swiper-item>
        <image
          src="../../static/tabbar/2.jpg"
          style="width: 750rpx; height: 250rpx"
        ></image>
      </swiper-item>
    </swiper>

    <!--列表-->
    <view class="flex flex-wrap">
      <view
        v-for="(item,index) in videos"
        :key="index"
        @click="openLive"
      >
        <fList :item="item"></fList>
      </view>
    </view>
  </view>
</template>

<script>
import fList from "../../components/common/f-list.vue";
export default {
  data() {
    return {
      videos: [
        {
          picture:
            "https://niit-student.oss-cn-beijing.aliyuncs.com/markdown/26.jpg",
          url: "https://live.utools.club/live/cPWGr3wJnLCme6FTmcOu.flv?sign=1604336190-13fb99534fbc4ac873377589087489ad",
          status: "已结束",
          people: 156,
          title: "肩部强化",
          price: 159,
        },
        {
          picture:
            "https://niit-student.oss-cn-beijing.aliyuncs.com/markdown/23.jpg",
          url: "*",
          status: "进行中",
          people: 3222,
          title: "综合体育",
          price: 333,
        },
        {
          picture:
            "https://niit-student.oss-cn-beijing.aliyuncs.com/markdown/21.jpg",
          url: "*",
          status: "已结束",
          people: 4421,
          title: "FE电动方程式",
          price: 112,
        },
        {
          picture:
            "https://niit-student.oss-cn-beijing.aliyuncs.com/markdown/20.jpg",
          url: "*",
          status: "进行中",
          people: 2435,
          title: "斯诺克",
          price: 865,
        },
        {
          picture:
            "https://niit-student.oss-cn-beijing.aliyuncs.com/markdown/18.jpg",
          url: "*",
          status: "已结束",
          people: 123,
          title: "搏击精选",
          price: 232,
        },
        {
          picture:
            "https://niit-student.oss-cn-beijing.aliyuncs.com/markdown/17.jpg",
          url: "*",
          status: "进行中",
          people: 123,
          title: "虎牙健身房",
          price: 232,
        },
      ],
    };
  },
  onLoad() {},
  methods: {
    openLive() {
      uni.navigateTo({
        url: "../live/live",
      });
    },
  },
  components: {
    fList,
  },
};
</script>

<style>
</style>
