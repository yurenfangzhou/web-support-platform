<template>
  <page-layout :avatar="avatar">
    <div slot="headerContent">
      <div class="title">{{ timeFix }}，{{ user.name }}，{{ welcome }}</div>
      <div>You are not alone.</div>
    </div>
    <div slot="extra">
      <a-row>
        <a-col :sm="8" :xs="24">
          <head-info title="可用节点" content="16" :bordered="true"/>
        </a-col>
        <a-col :sm="8" :xs="24">
          <head-info title="高级节点" content="7/16" :bordered="true"/>
        </a-col>
        <a-col :sm="8" :xs="24">
          <head-info title="剩余流量" content="2,23Gb"/>
        </a-col>
      </a-row>
    </div>

    <a-card :style="{ padding: '0 15%' }">
      <a-row :gutter="16">
        <a-col :md="24" :lg="8" :style="{ minHeight: '180px' }">
          <div class="ant-upload-preview" >
            <a-icon type="cloud-upload-o" class="upload-icon"/>
            <div class="mask">
              <a-icon type="plus" />
            </div>
            <img :src="option.img"/>
          </div>
        </a-col>
        <a-col :md="24" :lg="16">

          <a-form layout="vertical">
            <a-form-item
              label="昵称"
            >
              <a-input placeholder="给自己起个名字" />
            </a-form-item>
            <a-form-item
              label="Bio"
            >
              <a-textarea rows="4" placeholder="You are not alone."/>
            </a-form-item>

            <a-form-item
              label="电子邮件"
              :required="false"
            >
              <a-input placeholder="exp@admin.com"/>
            </a-form-item>
            <a-form-item
              label="加密方式"
              :required="false"
            >
              <a-select defaultValue="aes-256-cfb">
                <a-select-option value="aes-256-cfb">aes-256-cfb</a-select-option>
                <a-select-option value="aes-128-cfb">aes-128-cfb</a-select-option>
                <a-select-option value="chacha20">chacha20</a-select-option>
              </a-select>
            </a-form-item>
            <a-form-item
              label="连接密码"
              :required="false"
            >
              <a-input placeholder="h3gSbecd"/>
            </a-form-item>
            <a-form-item
              label="登陆密码"
              :required="false"
            >
              <a-input placeholder="密码"/>
            </a-form-item>

            <a-form-item>
              <a-button type="primary">提交</a-button>
              <a-button style="margin-left: 8px">保存</a-button>
            </a-form-item>
          </a-form>

        </a-col>
      </a-row>
    </a-card>

  </page-layout>
</template>

<script>
  import {timeFix, welcome} from "../../../utils/util"
  import LayoutMain from '@/components/layout/LayoutMain'
  import PageLayout from '@/components/layout/PageLayout'

  import HeadInfo from '@/components/tools/HeadInfo'
  import ASelect from "ant-design-vue/es/select";
  import AForm from "ant-design-vue/es/form/Form";
  import VueCropper from "vue-cropper/example/src/vue-cropper/vue-cropper";

  export default {
    name: "Index",
    components: {
      VueCropper,
      AForm,
      ASelect,
      LayoutMain,
      PageLayout,
      HeadInfo
    },
    data () {
      return {
        timeFix: timeFix(),
        welcome: welcome(),
        avatar: '',
        user: {},

        // cropper
        preview: {},
        option: {
          img: '/avatar2.jpg',
          info: true,
          size: 1,
          outputType: 'jpeg',
          canScale: false,
          autoCrop: true,
          // 只有自动截图开启 宽度高度才生效
          autoCropWidth: 180,
          autoCropHeight: 180,
          fixedBox: true,
          // 开启宽度和高度比例
          fixed: true,
          fixedNumber: [1, 1]
        }
      }
    },
    computed: {
      userInfo() {
        return this.$store.getters.userInfo
      }
    },
    created() {
      this.user = this.userInfo
      this.avatar = this.userInfo.avatar
    },
    methods: {

      realTime (data) {
        this.preview = data
      }
    }
  }
</script>

<style lang="scss" scoped>
  .avatar-upload-wrapper {
    height: 200px;
    width: 100%;
  }

  .ant-upload-preview {
    position: relative;
    margin: 0 auto;
    width: 100%;
    max-width: 180px;
    border-radius: 50%;
    box-shadow: 0 0 4px #ccc;

    .upload-icon {
      position: absolute;
      top: 0;
      right: 10px;
      font-size: 1.4rem;
      padding: 0.5rem;
      background: rgba(222, 221, 221, 0.7);
      border-radius: 50%;
      border: 1px solid rgba(0, 0, 0, 0.2);
    }
    .mask {
      opacity: 0;
      position: absolute;
      background: rgba(0,0,0,0.4);
      cursor: pointer;
      transition: opacity 0.4s;

      &:hover {
        opacity: 1;
      }

      i {
        font-size: 2rem;
        position: absolute;
        top: 50%;
        left: 50%;
        margin-left: -1rem;
        margin-top: -1rem;
        color: #d6d6d6;
      }
    }

    img, .mask {
      width: 100%;
      max-width: 180px;
      height: 100%;
      border-radius: 50%;
      overflow: hidden;
    }
  }
</style>