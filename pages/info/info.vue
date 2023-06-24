<template>
  <view class="content">
    <!-- <view style="height: 10px; background-color: #fff"></view> -->
    <view class="step-container">
      <uni-steps
        :options="[
          { title: '样本' },
          { title: '加做' },
          { title: '患者' },
          { title: '疑似' },
          { title: '临床' },
          { title: '送检' },
        ]"
        :active="1"
      ></uni-steps>
    </view>

    <!-- <uni-card :is-shadow="false" is-full>
      <text class="uni-h6"
        >uni-forms
        组件一般由输入框、选择器、单选框、多选框等控件组成，用以收集、校验、提交数据。</text
      >
    </uni-card> -->

    <uni-section title="个人信息" type="line">
      <view class="info">
        <uni-forms
          ref="baseForm"
          :model="baseFormData"
          label-width="80px"
          label-align="left"
        >
          <uni-forms-item label="姓名" required>
            <uni-easyinput
              v-model="baseFormData.name"
              placeholder="请输入姓名"
            />
          </uni-forms-item>
          <uni-forms-item label="年龄" required>
            <uni-easyinput
              v-model="baseFormData.name"
              placeholder="请输入年龄"
            />
          </uni-forms-item>
          <uni-forms-item label="身份证号" required>
            <uni-easyinput
              v-model="baseFormData.name"
              placeholder="请输入身份证号"
            />
          </uni-forms-item>
        </uni-forms>
      </view>
    </uni-section>

    <uni-section title="检测信息" type="line">
      <view class="info">
        <uni-forms
          ref="baseForm"
          :model="baseFormData"
          label-width="80px"
          label-align="left"
        >
          <uni-forms-item label="条形码" required>
            <uni-easyinput
              v-model="baseFormData.name"
              placeholder="请输入条形码"
              suffixIcon="scan"
              @iconClick="scan"
            />
          </uni-forms-item>
          <uni-forms-item label="检测项目">
            <uni-data-select
              :localdata="baseFormData.detectionItems"
              v-model="detectionItem"
              label="检测项目"
              @change="change"
            ></uni-data-select>
          </uni-forms-item>
          <uni-forms-item label="样本类型">
            <uni-data-select :localdata="baseFormData.detectionItems" />
          </uni-forms-item>

          <uni-forms-item label="送检时间">
            <uni-datetime-picker
              type="datetime"
              return-type="timestamp"
              v-model="baseFormData.datetimesingle"
            />
          </uni-forms-item>
        </uni-forms>
      </view>
    </uni-section>

    <uni-section title="上传样本图片" type="line">
      <view class="example-body">
        <uni-file-picker limit="9" title="最多选择9张图片"></uni-file-picker>
      </view>
    </uni-section>
    <button class="next-button">下一步</button>
    <view style="height: 100px"></view>
  </view>
</template>
<script>
export default {
  data() {
    return {
      // 基础表单数据
      baseFormData: {
        name: "",
        age: "",
        introduction: "",
        sex: 2,
        hobby: [5],
        datetimesingle: 1627529992399,
        detectionItems: [
          { text: "DNA+RNA", value: 0 },
          { text: "DNA", value: 1 },
        ],
      },
      // 表单数据
      alignmentFormData: {
        name: "",
        age: "",
      },
      detectionItem: "",
      // 单选数据源
      sexs: [
        {
          text: "男",
          value: 0,
        },
        {
          text: "女",
          value: 1,
        },
        {
          text: "保密",
          value: 2,
        },
      ],
      // 多选数据源
      hobbys: [
        {
          text: "跑步",
          value: 0,
        },
        {
          text: "游泳",
          value: 1,
        },
        {
          text: "绘画",
          value: 2,
        },
        {
          text: "足球",
          value: 3,
        },
        {
          text: "篮球",
          value: 4,
        },
        {
          text: "其他",
          value: 5,
        },
      ],
      // 分段器数据
      current: 0,
      items: ["左对齐", "顶部对齐"],
      // 校验表单数据
      valiFormData: {
        name: "",
        age: "",
        introduction: "",
      },
      // 校验规则
      rules: {
        name: {
          rules: [
            {
              required: true,
              errorMessage: "姓名不能为空",
            },
          ],
        },
        age: {
          rules: [
            {
              required: true,
              errorMessage: "年龄不能为空",
            },
            {
              format: "number",
              errorMessage: "年龄只能输入数字",
            },
          ],
        },
      },
      // 自定义表单数据
      customFormData: {
        name: "",
        age: "",
        hobby: [],
      },
      // 自定义表单校验规则
      customRules: {
        name: {
          rules: [
            {
              required: true,
              errorMessage: "姓名不能为空",
            },
          ],
        },
        age: {
          rules: [
            {
              required: true,
              errorMessage: "年龄不能为空",
            },
          ],
        },
        hobby: {
          rules: [
            {
              format: "array",
            },
            {
              validateFunction: function (rule, value, data, callback) {
                if (value.length < 2) {
                  callback("请至少勾选两个兴趣爱好");
                }
                return true;
              },
            },
          ],
        },
      },
      dynamicFormData: {
        email: "",
        domains: {},
      },
      dynamicLists: [],
      dynamicRules: {
        email: {
          rules: [
            {
              required: true,
              errorMessage: "域名不能为空",
            },
            {
              format: "email",
              errorMessage: "域名格式错误",
            },
          ],
        },
      },
    };
  },
  computed: {
    // 处理表单排列切换
    alignment() {
      if (this.current === 0) return "left";
      if (this.current === 1) return "top";
      return "left";
    },
  },
  onLoad() {},
  onReady() {
    // 设置自定义表单校验规则，必须在节点渲染完毕后执行
    // this.$refs.customForm.setRules(this.customRules);
  },
  methods: {
    scan(e) {
      uni.scanCode({
        success: function (res) {
          console.log("条码类型：" + res.scanType);
          console.log("条码内容：" + res.result);
        },
      });
    },
    change(e) {
      console.log(e);
    },
    onClickItem(e) {
      console.log(e);
      this.current = e.currentIndex;
    },
    add() {
      this.dynamicLists.push({
        label: "域名",
        rules: [
          {
            required: true,
            errorMessage: "域名项必填",
          },
        ],
        id: Date.now(),
      });
    },
    del(id) {
      let index = this.dynamicLists.findIndex((v) => v.id === id);
      this.dynamicLists.splice(index, 1);
    },
    submit(ref) {
      this.$refs[ref]
        .validate()
        .then((res) => {
          console.log("success", res);
          uni.showToast({
            title: `校验通过`,
          });
        })
        .catch((err) => {
          console.log("err", err);
        });
    },
  },
};
</script>

<style lang="scss">
@import "../../common/uni.css";
.step-container {
  height: 50px;
  padding-top: 10px;
  background-color: #fff;
}
.uni-mt-5 {
  margin-top: 5px;
}
.uni-form-item {
  display: inline-block;
}

.info {
  padding-left: 15px;
  padding-right: 15px;
  padding-bottom: 10px;
  background-color: #fff;
}

.segmented-control {
  margin-bottom: 10px;
}

.button-group {
  margin-top: 15px;
  display: flex;
  justify-content: space-around;
}

.form-item {
  display: flex;
  align-items: center;
}

.next-button {
  display: flex;
  align-items: center;
  height: 30px;
  margin: 20px;
  // background: #2c53fe;
  background-color: #007bff;
  color: #fff;
  text-align: center;
  display: flex;
  justify-content: center;
  font-size: smaller;
}

.example-body {
  padding: 10px;
  padding-top: 0;
}

.custom-image-box {
  /* #ifndef APP-NVUE */
  display: flex;
  /* #endif */
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
}

.text {
  font-size: 14px;
  color: #333;
}
</style>
