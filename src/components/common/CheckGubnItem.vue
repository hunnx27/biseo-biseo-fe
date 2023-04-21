<template>
  <div class="step-one page-wrap">
    <div class="radio-wrap">
      <label for="checkJobGubn1">
        <input
          id="checkJobGubn1"
          v-model="gubn"
          name="gubn"
          type="radio"
          value="B"
          @change="stored($event)"
        /> 비서<br />
      </label>
      <p v-show="gubn == 'B'"><b>현재 비서로 일하고 있는 진짜 비서 : </b><br/>비서비서의 모든 기능을 이용할 수 있어요.</p>
    </div>
    <div class="radio-wrap">
      <label for="checkJobGubn2">
        <input
          id="checkJobGubn2"
          v-model="gubn"
          name="gubn"
          type="radio"
          value="N"
          @change="stored($event)"
        /> 노비서<br />
      </label>
      <p v-show="gubn == 'N'"><b>비서가 되고 싶은 사람 예비 비서 : </b><br/>비서비서에서 리스트 조회만 가능해요.</p>
    </div>
  </div>
</template>

<script>
import { mapActions, mapGetters, mapMutations } from "vuex";

export default {
  name: "StepOneItem",
  components: {},
  props: {},
  data() {
    return {
      gubn: null,
    };
  },
  methods: {
    ...mapActions(["setSignupGubn"]),
    stored(e) {
      console.log(e.target.value);
      const gubn = e.target.value;
      this.setSignupGubn({ gubn });
    },
  },
  created: function () {
    // Appbar Option 설정
    // const options = {isShowCheckBtn: false,isShowNextBtn: true,isShowSearchBtn: false};
    // this.$emit('setLayout',options);

    if (this.signupData != null) {
      this.gubn = this.signupData != null ? this.signupData.gubnCode : null;
    } else {
      this.gubn = null;
    }
  },
};
</script>

<style lang="scss" scoped>
.radio-wrap {
  align-items: center;
  margin-top: 10px;
  padding: 10px 10px;
  background: #fff;
  border: 1px solid #673ab7;
  border-radius: 10px;
}
</style>
