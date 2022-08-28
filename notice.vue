<template>
  <view v-if="popupShow" >
    <view class="popup-bg"></view>
    <view class="popup-box">
      <view class="child-popup-quantificationType">
        <img src="../static/images/img_notice.png" class="child-popup-quantificationType-img">
<!--        {{ $t('message.notice') }}-->
      </view>
      <view class="content" >
        <view v-html="content.title">
        </view>
        <view class="submit-btns">
          <view class="submit-btn submit-btn1" @click="confirm(1)">确定</view>
        </view>
      </view>
    </view>

    <view class="popup-img-bg" v-if="popupImShow" @click="popupImShow = false"></view>
    <img class="popup-img-box" :src="popupImgSrc" v-if="popupImShow">

  </view>
</template>

<script>
// 使用的页面
// import notice from '@/components/notice';
/*components: {
      notice,
},*/
// data里面
/*noticeShow: false,
    noticeContent: {
  title: '公告内容'
},*/
// <notice :popupShow="noticeShow" :content="noticeContent"  @onHandler="onConfirm"></notice>
// 公告
/*onConfirm (type) {
    this.noticeShow = false
},*/
export default {
  components: {

  },
  props: {
    popupShow: false,
    content: {},
  },
  data() {
    return {
      popupImShow: false,
      popupImgSrc: '',
    };
  },
  watch: {
    popupShow () {
      this.$nextTick(() => {
        let imgs = document.getElementsByClassName('content')[0].getElementsByTagName('img')

        for (const item of imgs) {
          item.onclick = () => {
            this.popupImgSrc = item.getAttribute('src')
            this.popupImShow = true
          }
        }
      })

    }
  },
  computed: {},
  created() {

  },
  mounted() {

  },
  methods: {
    confirm(type) {
      this.$emit('onHandler', type)
    },
    showPopupImg(src) {
      this.popupImgSrc = src
      this.popupImShow = true
    }
  },
};
</script>

<style scoped lang="scss">
.popup-bg{
  position: fixed;
  left: 0;
  top: 0;
  height: 100vh;
  width: 100%;
  z-index: 10000;
  background: rgba(0,0,0,.5);
}
.popup-box{
  position: fixed;
  left: 50%;
  top: 50%;
  z-index: 10001;
  transform: translate(-50%, -50%);
  border-radius: 10px;
  overflow: hidden;

}
.popup-box{
  width: 90%;
  text-align: center;
  overflow: hidden;
  .child-popup-quantificationType{
  min-height: 60px;
    background: #21AD82;
    font-size: 16px;
    font-weight: bold;
    text-align: center;
    color: #139782;
  }
  .content{
    text-align: left;
    padding:10px 10px 30px 10px;
    word-break: break-all;
    line-height: 15px;
    background: #fff;
    font-size: 13px;
    max-height: 55vh;
    overflow: auto;
    font-family: SimHei,Helvetica Neue,Arial,Droid Sans,sans-serif;

  }

  .content ::v-deep img{
    margin: 5px 0;
    max-width: 100% !important;
    width: 100%;
  }
  .content-img{
    margin: 8px 0;
    width: 100%;
  }

  .submit-btns{
    display: flex;
  }
  .submit-btn{
    margin:25px auto 0;
    width:170px;
    border-radius: 30px;
    background: #40A57B;
    font-size: 15px;
    color: #fff;
    text-align: center;
    height: 33px;
    line-height: 33px;
  }
  .submit-btn:nth-child(2) {
    margin-left: 10px;
  }
  .submit-btn1{
    animation: submitBtnA 1s infinite;
  }
}
@keyframes submitBtnA {
  0%{
    transform: scale(0.8);
  }
  50%{
    transform: scale(1);
  }
  100%{
    transform: scale(0.8);
  }
}

.popup-img-bg{
  position: fixed;
  left: 0;
  top: 0;
  height: 100vh;
  width: 100%;
  z-index: 999;
  background: rgba(0,0,0,1);
}
.popup-img-box{
  position: fixed;
  left: 50%;
  top: 50%;
  max-height: 70%;
  z-index: 1000;
  transform: translate(-50%, -50%);
}

.child-popup-quantificationType-img{
  width: 100%;
  display: block;
}


</style>
