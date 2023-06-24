<template>
  <view class="content">
    <uni-section title="查询检测记录" type="line">
      <view class="search">
        <uni-search-bar
          class="search-input"
          @confirm="search"
          placeholder="请输入身份证号"
          :focus="true"
          v-model="searchValue"
          @blur="blur"
          @focus="focus"
          @input="input"
          @cancel="cancel"
          @clear="clear"
          cancelButton="none"
        >
        </uni-search-bar>
        <!-- <view class="search-result">
          <text class="search-result-text">当前输入为：{{ searchValue }}</text>
        </view> -->
      </view>

      <view class="result-list">
        <uni-list>
          <uni-list-item
            title="检测报告1"
            note="DNA"
            thumb="/static/download.png"
            thumbSize="lg"
            rightText="2023-06-22"
          ></uni-list-item>
        </uni-list>
        <uni-list>
          <uni-list-item
            title="检测报告2"
            note="DNA+RNA"
            thumb="/static/download.png"
            thumbSize="lg"
            rightText="2023-06-23"
          ></uni-list-item>
        </uni-list>
      </view>
    </uni-section>
  </view>
</template>

<script>
export default {
  data() {
    return {
      searchValue: "",
    };
  },
  methods: {
    search(res) {
      uni.showToast({
        title: "搜索：" + res.value,
        icon: "none",
      });
    },
    input(res) {
      console.log("----input:", res);
    },
    clear(res) {
      uni.showToast({
        title: "clear事件，清除值为：" + res.value,
        icon: "none",
      });
    },
    blur(res) {
      uni.showToast({
        title: "blur事件，输入值为：" + res.value,
        icon: "none",
      });
    },
    focus(e) {
      uni.showToast({
        title: "focus事件，输出值为：" + e.value,
        icon: "none",
      });
    },
    cancel(res) {
      uni.showToast({
        title: "点击取消，输入值为：" + res.value,
        icon: "none",
      });
    },
    // download(res) {
    //   uni.chooseImage({
    //     success: function (res) {
    //       var tempFilePaths = res.tempFilePaths;
    //       uni.saveFile({
    //         tempFilePath: tempFilePaths[0],
    //         success: function (res) {
    //           var savedFilePath = res.savedFilePath;
    //         },
    //       });
    //     },
    //   });
    // },
  },
  onBackPress() {
    // #ifdef APP-PLUS
    plus.key.hideSoftKeybord();
    // #endif
  },
};
</script>

<style lang="scss">
.search {
  padding: 15px;
  padding-top: 0;
  background-color: #fff;
}

.search-input {
  height: 30px;
  //   text-align: center;
}

.search-result {
  padding-top: 10px;
  padding-bottom: 20px;
  text-align: center;
}

.search-result-text {
  text-align: center;
  font-size: 14px;
  color: #666;
}

.example-body {
  /* #ifndef APP-NVUE */
  display: block;
  /* #endif */
  padding: 0px;
}

.uni-mt-10 {
  margin-top: 10px;
}
</style>
