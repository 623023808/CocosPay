<template>
  <div class="app-container">
    <navigation :title="$t('title.sendDetail')"/>
    <div class="eos-main">
      <h2
        class="eos-style cocos mt20"
      >{{cocosAccount.accounts === orderDeatil.parse_operations.from ? '-' : '+'}}{{orderDeatil.parse_operations.amount}}</h2>
      <div class="des">{{$t('alert.tranferSuccess')}}</div>
      <div class="translate-log-title mt40">
        <div class="log-line"></div>
        <!-- <div class="log-title">{{$t('title.history')}}</div>-->
      </div>
    </div>
    <div class="running">
      <div class="title mt20">
        <div class="key">{{$t('label.send')}}:</div>
        <div class="name">
          <p>{{orderDeatil.parse_operations.from}}</p>
          <button
            v-clipboard:copy="orderDeatil.parse_operations.from"
            v-clipboard:success="copySuccess"
            v-clipboard:error="copyError"
            type="button"
            style="margin-left:10px"
          ></button>
        </div>
      </div>

      <div class="title mt20">
        <div class="key">{{$t('label.receive')}}:</div>
        <div class="name">
          <p>{{orderDeatil.parse_operations.to}}</p>
          <button
            v-clipboard:copy="orderDeatil.parse_operations.to"
            v-clipboard:success="copySuccess"
            v-clipboard:error="copyError"
            type="button"
            style="margin-left:10px"
          ></button>
        </div>
      </div>
    </div>
    <div class="eos-main">
      <div class="translate-log-title mt10">
        <div class="log-line"></div>
        <!-- <div class="log-title">{{$t('title.history')}}</div>-->
      </div>
    </div>
    <div class="running mt15">
      <div class="title mt20">
        <div class="key">{{$t('label.hash')}}:</div>
        <div class="name">{{orderDeatil.id}}</div>
      </div>

      <div class="title mt20">
        <div class="key">{{$t('label.blockHeight')}}:</div>
        <div class="name">{{orderDeatil.block_num}}</div>
      </div>

      <div class="title mt20">
        <div class="key">{{$t('label.tradeTime')}}:</div>
        <div class="name">{{orderDeatil.date}}</div>
      </div>
    </div>
  </div>
</template>
<script>
import Navigation from "../../components/navigation";
import utils from "../../../lib/utils";
import { mapState, mapActions, mapMutations } from "vuex";
export default {
  components: {
    Navigation
  },
  data() {
    return {
      orderDeatil: {}
    };
  },
  computed: {
    ...mapState(["cocosAccount"])
  },
  created() {
    this.orderDeatil = this.$route.params;
  },
  methods: {
    copySuccess() {
      this.$kalert({
        message: this.$i18n.t("alert.copySuccess")
      });
    },
    copyError() {
      this.$kalert({
        message: this.$i18n.t("alert.copyFail")
      });
    }
  }
};
</script>
<style lang="scss" scoped>
@import "../../styles/home.scss";
.cocos {
  font-size: 22px;
  font-family: NotoSansHans-Medium;
  font-weight: 500;
  color: rgba(70, 121, 254, 1);
}
.eos-style {
  margin-bottom: 0 !important;
}
.eos-main {
  border-top: none !important;
}
.des {
  color: #8c9097;
  font-size: 15px;
  font-family: NotoSansHans-Regular;
  font-weight: 400;
  color: rgba(140, 144, 151, 1);
}
.mt40 {
  margin-top: 40px;
}
.running {
  display: flex;
  flex-direction: column;
  .key {
    width: 100px;
  }
  .title {
    display: flex;
    align-items: center;
    color: #8c9097;
    font-size: 15px;
  }
  .name {
    display: flex;
    font-size: 15px;
    align-items: center;
    button {
      height: 16px;
      width: 16px;
      background: url("/icons/copy.png") no-repeat center;
      background-size: 100% 100%;
      margin-left: 5px;
      margin: 0;
      padding: 0;
      border: none; //自定义边框
      outline: none;
    }
  }
}
</style>
