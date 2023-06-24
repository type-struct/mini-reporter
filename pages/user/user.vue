<template>
  <view class="content">
    <view class="logo-container">
      <image size="50px" class="logo" src="/static/nasa-logo.svg"></image>
    </view>
    <view class="user-management">
      <uni-grid
        :column="4"
        :highlight="true"
        @change="change"
        :show-border="false"
      >
        <uni-grid-item>
          <view class="grid-item-box">
            <uni-icons type="person-filled" size="25" />
            <text class="text">个人信息</text>
          </view>
        </uni-grid-item>
        <uni-grid-item>
          <view class="grid-item-box">
            <uni-icons type="heart-filled" size="25" />
            <text class="text">公益</text>
          </view>
        </uni-grid-item>
        <uni-grid-item>
          <view class="grid-item-box">
            <uni-icons type="settings-filled" size="25" />
            <text class="text">设置</text>
          </view>
        </uni-grid-item>
        <uni-grid-item>
          <view class="grid-item-box">
            <uni-icons type="notification" size="25" />
            <text class="text">通知</text>
          </view>
        </uni-grid-item>
      </uni-grid>
    </view>
    <view class="feedback-container">
      <!-- <view class="feedback"> -->
      <uni-list class="list-container" border="true">
        <view class="uni-list-item">
          <uni-list-item
            title="用户意见反馈"
            clickable
            showArrow
            link="navigateTo"
            to="'/pages/index/index'"
            @click="onClick"
            ><view class="uni-list-content"></view
          ></uni-list-item>
        </view>
        <uni-list-item title="其他" clickable></uni-list-item>
      </uni-list>
      <!-- </view> -->
    </view>
    <!-- <view class="login-button-container">
      <view class="login-button" @click="login">登陆</view>
    </view> -->
    <button class="login-button" @click="login">登陆</button>
  </view>
</template>

<script>
export default {
  components: {},
  data() {
    return {
      dynamicList: [],
    };
  },
  methods: {
    login(e) {
      uni.showToast({
        title: `登陆`,
        icon: "none",
      });
    },
    onClick(e) {
      console.log(e);
      uni.navigateTo({ url: "/pages/index/index" });
    },
    change(e) {
      let { index } = e.detail;
      this.list[index].badge && this.list[index].badge++;

      uni.showToast({
        title: `点击第${index + 1}个宫格`,
        icon: "none",
      });
    },
    add() {
      if (this.dynamicList.length < 9) {
        this.dynamicList.push({
          url: `/static/c${this.dynamicList.length + 1}.png`,
          text: `Grid ${this.dynamicList.length + 1}`,
          color: this.dynamicList.length % 2 === 0 ? "#f5f5f5" : "#fff",
        });
      } else {
        uni.showToast({
          title: "最多添加9个",
          icon: "none",
        });
      }
    },
    del() {
      this.dynamicList.splice(this.dynamicList.length - 1, 1);
    },
  },
};
</script>

<style lang="scss">
.logo-container {
  height: 200px;
  width: 100%;
  align-items: center;
  display: flex;
  justify-content: center;
  // background-color: cyan;
}

.logo {
  width: 100px;
  height: 100px;
}

.user-management {
  margin: 10px;
  border-radius: 8px;
  background-color: #fff;
  box-shadow: 0px 0px 4px 2px rgba(205, 205, 207, 0.5);
}

.feedback-container {
  margin: 10px;
  border-radius: 8px;
  background-color: #fff;
  box-shadow: 0px 0px 4px 2px rgba(205, 205, 207, 0.5);
}

.uni-list-item,
.uni-list,
.grid-item-box {
  background-color: transparent !important;
}

.image {
  width: 25px;
  height: 25px;
}

.login-button-container {
  margin-top: 10px;
  margin: 10px;
  border-radius: 8px;

  // margin-right: 30px;
  // background-color: #f01212;
  // border-style: none;
  box-shadow: 0px 0px 4px 2px rgba(205, 205, 207, 0.5);
}

// .login-button {
//   align-items: center;
//   display: flex;
//   justify-content: center;
//   height: 30px;
//   border-radius: 8px;
//   background-color: #3466fb;
//   color: white;
// }

// .login-button:active {
//   background-color: #9b9a9a;
// }

button {
  font-size: smaller;
  background-color: #3466fb;
  margin-left: 10px;
  margin-right: 10px;
  border-radius: 8px;
  color: white;
}

.text {
  font-size: 14px;
  margin-top: 5px;
}

.grid-dynamic-box {
  margin-bottom: 15px;
}

.grid-item-box {
  flex: 1;
  // position: relative;
  /* #ifndef APP-NVUE */
  display: flex;
  /* #endif */
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 15px 0;
}

.grid-item-box-row {
  flex: 1;
  // position: relative;
  /* #ifndef APP-NVUE */
  display: flex;
  /* #endif */
  flex-direction: row;
  align-items: center;
  justify-content: center;
  padding: 15px 0;
}

.grid-dot {
  position: absolute;
  top: 5px;
  right: 15px;
}

.swiper {
  height: 420px;
}

/* #ifdef H5 */
@media screen and (min-width: 768px) and (max-width: 1425px) {
  .swiper {
    height: 630px;
  }
}

@media screen and (min-width: 1425px) {
  .swiper {
    height: 830px;
  }
}

/* #endif */
</style>
