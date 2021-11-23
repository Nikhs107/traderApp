<template>
  <div>
    <article class="message" :class="accordianClasses">
      <div class="message-header" @click="toggleAccordion">
        <div class="row">
          <div class="icon">
            <div class="circle"><i class="fas fa-dollar-sign fa-3x"></i></div>
          </div>
          <div class="icon-text">
            <div :style="{ float: 'left' }">
              <b>Review Payment Options</b><i>(Optional)</i>
            </div>
            <div :style="{ float: 'right' }">
              <span class="angle" v-show="isOpen"
                ><i class="fas fa-angle-up fa-lg"></i
              ></span>
              <span class="angle" v-show="!isOpen"
                ><i class="fas fa-angle-down fa-lg"></i
              ></span>
            </div>
          </div>
        </div>
      </div>
      <div class="message-body">
        <div class="message-content">
          Select a Payment Option:
          <div
            class="container mt-2"
            :class="financePay === false ? 'back' : ''"
            @click="changePay(false)"
          >
            <input
              type="radio"
              name="paymentOption"
              id="cash"
              class="ms-3"
              v-model="data.cash"
              @input="getData"
              @click="changePay(false)"
            />
            <label class="px-2" for="cash">Cash</label>
          </div>
          <br />
          <div
            class="container"
            :class="financePay === true ? 'back' : ''"
            @click="changePay(true)"
          >
            <input
              type="radio"
              name="paymentOption"
              id="finance"
              class="ms-3"
              checked
              @click="changePay(true)"
            />
            <label class="px-2" for="finance">Finance</label>
            <div v-show="financePay">
              <hr class="ms-3" />
              <div class="ddPay col-md-7 col-xs-11">
                <Dropdown
                  label="Hows your Credit?"
                  :list="credits"
                  :getDDval="assignCredit"
                  :ddBack="true"
                />
              </div>
              <br />
              <strong class="p-3">Estimated Monthly Payment</strong>
              <hr class="ms-3" />
              <div class="row ms-3 me-3">
                <div class="col-md-6 col-xs-12">
                  <div class="row">
                    <div class="col-md-5 col-xs-12">
                      <label for="downPay" class="payLabel">
                        Down Payment</label
                      >
                    </div>
                    <div class="col-md-7 col-xs-12">
                      <input
                        type="text"
                        class="textbox"
                        id="downPay"
                        v-model="data.downPay"
                        @change="getData"
                      />
                    </div>
                  </div>
                  <div class="slider">
                    <input
                      class="sliderBar"
                      type="range"
                      min="0"
                      max="8000"
                      value="4000"
                      v-model="slider1Value"
                      @change="putValue"
                    />
                  </div>
                  <h5 class="warning">{{ slider1Value }}</h5>
                </div>
                <div class="col-md-6 col-xs-12">
                  <div class="row">
                    <div class="col-md-5 col-xs-12">
                      <label for="term" class="payLabel"> Term (months)</label>
                    </div>
                    <div class="col-md-7 col-xs-12">
                      <input
                        type="text"
                        class="textbox"
                        id="term"
                        v-model="data.terms"
                        @change="getData"
                      />
                    </div>
                  </div>
                  <div class="slider">
                    <input
                      class="sliderBar"
                      type="range"
                      min="24"
                      max="72"
                      value="48"
                      step="12"
                      list="ticks1"
                      v-model="slider2Value"
                      @change="putValue"
                    />
                    <datalist id="ticks1">
                      <option value="24">24</option>
                      <option value="36">36</option>
                      <option value="48">48</option>
                      <option value="60">60</option>
                      <option value="72">72</option>
                    </datalist>
                  </div>
                </div>
              </div>
              <div class="disc ms-3">
                <a href="#" @click="handleDisc">Disclaimer</a>
                <p v-show="disclaimer">
                  This monthly payment estimate is based solely on the credit
                  and other information you have provided and is for
                  informational purposes only. The monthly estimate does not
                  represent a financing offer from the seller of this vehicle or
                  from any third party, and we do not and will not disclose this
                  estimate (or any other information you have provided) to any
                  third-party providers of financing or credit. This estimate
                  does not include any title or other fees and incentives, and
                  other taxes may apply to the actual monthly payment. The
                  actual monthly payment for this vehicle may be significantly
                  different from this estimate.
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </article>
  </div>
</template>

<script>
import Dropdown from "./Dropdown.vue";

export default {
  name: "Payment",
  props: {
    getDDval: Function,
  },
  components: {
    Dropdown,
  },
  data() {
    return {
      data: {
        cash: false,
        credits: "",
        downPay: "",
        terms: "",
      },
      isOpen: false,
      credits: [
        "Excellent(720-850)",
        "Good(690-719)",
        "Fair(630-689)",
        "Repairing(300-629)",
      ],
      financePay: true,
      disclaimer: false,
      slider1Value: "",
      slider2Value: 48,
    };
  },
  methods: {
    toggleAccordion() {
      this.isOpen = !this.isOpen;
    },
    handleClick(id) {
      this.tradeIn = id === "no" ? false : true;
      if (id === "no") {
        document.getElementById(id).className = "active";
        document.getElementById("yes").className = "check";
      } else {
        document.getElementById(id).className = "active";
        document.getElementById("no").className = "check";
      }
    },
    putValue() {
      this.data.terms = this.slider2Value;
      this.data.downPay = this.slider1Value;
      this.getData();
    },
    changePay(choice) {
      this.financePay = choice;
      document.getElementById("cash").checked = !choice;
      document.getElementById("finance").checked = choice;
    },
    handleDisc() {
      this.disclaimer = !this.disclaimer;
    },
    getData() {
      this.$emit("payData", this.data);
    },
    assignCredit(val) {
      this.data.credits = val;
      this.getData();
    },
  },
  computed: {
    accordianClasses() {
      return {
        "is-closed": !this.isOpen,
      };
    },
  },
};
</script>

<style scoped>
.message-content {
  padding-right: 30px;
  margin-left: 15px;
  padding-top: 10px;
}
.check,
.active {
  width: 30%;
  cursor: pointer;
  margin-top: 15px;
  margin-bottom: 15px;
  padding: 15px;
  border: 1px solid black;
  border-radius: 5px;
}
.check {
  background: white;
}
.active {
  background: #b5251920;
  border: solid #b52519;
}
.container {
  border: 1px solid black;
  padding: 15px 5px;
  border-radius: 5px;
}
.fa-dollar-sign {
  font-size: 1.6em;
  width: 1.6em;
  text-align: center;
  line-height: 1.6em;
  color: darkred;
  padding-top: 10px;
  padding-left: 0px;
  padding-right: 2px;
}
.disc {
  margin: 0px 10px;
}
.disc > p {
  margin-top: 10px;
  text-align: justify;
}
.back {
  background-color: #f0f0f0;
}
.textbox {
  padding: 10px;
  border-radius: 5px;
  width: 100%;
}
.payLabel {
  padding: 10px 0px;
}
.slider {
  margin-top: 15px;
}
.sliderBar {
  width: 100%;
}
datalist {
  display: flex;
  justify-content: space-between;
  overflow: hidden;
}
.ddPay {
  margin: 20px;
  margin-top: 35px;
}
</style>
