<template>
  <view>
    <view class="top flex align-center justify-center"></view>

    <!--未登录-->
    <view
      v-if="!user"
      class="flex align-center"
    >
      <view
        class="flex align-center justify-center position-relative"
        style="width:180rpx;height:160rpx;"
      >
        <image
          src="https://niit-student.oss-cn-beijing.aliyuncs.com/markdown/333.jpg"
          class="rounded-circle"
          style="width:145rpx; height:145rpx; position:absolute; top:-60rpx;"
        ></image>
      </view>
      <view class="flex flex-column">
        <text class="font-md">未登录</text>
        <text class="font text-muted">登录体验更多功能</text>
      </view>
      <view class="ml-auto mr-3">
        <view
          class="border border-main rounded flex align-center justify-center p-2"
          hover-class="bg-light"
          @click="openLogin"
        ><text class="text-main font">立即登录</text></view>
      </view>
    </view>
    <!--已登录-->
    <view v-else>
      <view class="flex align-center">
        <view
          class="flex align-center justify-center position-relative"
          style="width:180rpx;height:160rpx;"
        >
          <image
            :src="user.avatar || '/static/img/1.jpg'"
            class="rounded-circle"
            style="width:130rpx; height:130rpx; position:absolute; top:-60rpx;"
          ></image>
        </view>
        <view class="flex flex-column">
          <text class="font-md">{{user.username}}</text>
          <text class="font text-muted">软件1851</text>
        </view>
        <view class="ml-auto mr-3">
          <view
            class="border border-main rounded flex align-center justify-center p-2"
            hover-class="bg-light"
          ><text class="text-main font">编辑资料</text></view>
        </view>
      </view>
      <view class="f-divider"></view>
      <f-list-item
        icon="iconbizhongguanli"
        title="我的金币"
        :showRight="false"
      ><text class="text-muted font">{{user ? user.coin : 0}}金币 立即充值</text></f-list-item>

      <f-list-item
        icon="iconzhengzaizhibo"
        title="我的直播"
      ><text class="text-muted font">0</text></f-list-item>

      <f-list-item
        icon="iconfaxian"
        title="我的关注"
      ><text class="text-muted font">0</text></f-list-item>
      <f-list-item
        icon="iconmore"
        title="历史记录"
      ></f-list-item>
      <f-list-item
        icon="icontuichu"
        title="退出"
        @click="logout"
      ></f-list-item>
	  <navigator open-type="navigate" url="../live-room/live-text">sss</navigator>
    </view>

  </view>
</template>

<script>
import fListItem from "@/components/common/f-list-item.vue";
import { mapState } from "vuex";
export default {
  data() {
    return {
      statusBarHeight: 0,
    };
  },
  components: {
    fListItem,
  },
  onLoad() {
    let res = uni.getSystemInfoSync();
    this.statusBarHeight = res.statusBarHeight;
  },
  onShow() {
    this.$store.dispatch("getUserInfo");
  },
  created() {},
  mounted() {},
  methods: {
    openLogin() {
      uni.navigateTo({
        url: "../login/login",
      });
    },
    logout() {
      this.$store.dispatch("logout").then((res) => {
        uni.navigateBack({
          delta: 1,
        });
      });
    },
  },
  computed: {
    ...mapState({
      user: (state) => state.user,
    }),
  },
};
</script>

<style scoped>
.top {
  width: 750rpx;
  height: 260rpx;
  background-image: url(../../static/img/1.jpg);
  background-size: cover;
  background-image: linear-gradient(to right, #ba7ace 0%, #8745ff 100%);
}
</style>
