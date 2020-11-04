<template>
  <view class="list-item">
    <image
      :src="item.picture"
      style="width: 365rpx; height: 365rpx"
      class="rounded"
      mode="aspectFill"
    ></image>

    <!--主播封面顶部左侧-->
    <view
      class="rounded-circle px-2 flex align-center"
      style="
        position: absolute;
        left: 15rpx;
        top: 15rpx;
        background-color: rgba(0, 0, 0, 0.4);
      "
    >
      <text class="iconfont iconbizhongguanli text-warning mr-1"></text>
      <text class="text-white font">{{item.price}}</text>
    </view>

    <!--主播封面顶部右侧人气-->
    <view
      class="rounded-circle px-2 flex align-center"
      style="
        position: absolute;
        right: 15rpx;
        top: 15rpx;
        background-color: rgba(0, 0, 0, 0.4);
      "
    >
      <text class="font-sm text-white">人气：</text>
      <text class="text-white font-sm">{{item.people}}</text>
    </view>

    <!--主播封面底部左侧标题内容-->
    <view
      class="rounded-circle flex align-center"
      style="position: absolute; left: 15rpx; bottom: 15rpx"
    >
      <text class="text-white font">{{item.title}}</text>
    </view>

    <!--主播封面底部左侧标题内容-->
    <view
      class="rounded-circle px-2 flex align-center"
      style="
        position: absolute;
        right: 15rpx;
        bottom: 15rpx;
        background-color: rgba(0, 0, 0, 0.4);
      "
    >
      <text
        style="width: 20rpx; height: 20rpx"
        class="rounded-circle bg-danger mr-1"
        v-if="item.status=='已结束'"
      ></text>
      <text
        style="width: 20rpx; height: 20rpx"
        class="rounded-circle bg-success mr-1"
        v-if="item.status=='进行中'"
      ></text>
      <text class="text-white font-sm">{{item.status}}</text>
    </view>
  </view>
</template>

<script>
export default {
  name: "f-list",
  props: {
    item: {},
  },
  onLoad() {
    console.log(item);
  },
  components: {},
  created() {},
  mounted() {},
  methods: {},
  computed: {},
};
</script>

<style scoped>
.list-item {
  width: 375rpx;
  height: 375rpx;
  padding: 5rpx;
  box-sizing: border-box;
  position: relative;
}
</style>
