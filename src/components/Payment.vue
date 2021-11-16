<template>
  <div>
    <article class="message" :class="accordianClasses">
      <div class="message-header" @click="toggleAccordion">
        <i class="fas fa-dollar-sign fa-lg"></i>
        <span class="icon-text"
          ><b>Review Payment Options</b><i>(Optional)</i></span
        >
        <button
          :style="{
            float: 'right',
            border: 'none',
            background: 'transparent',
          }"
        >
          <i class="fas" :class="isOpen ? 'fa-angle-up' : 'fa-angle-down'"></i>
        </button>
      </div>
      <div class="message-body">
        <div class="message-content">
          Select a Payment Option:
          <div class="container mt-2" :class="financePay === false ? 'back' : ''" @click="changePay(false)">
            <input
              type="radio"
              name="paymentOption"
              id="cash"
              class="ms-3"
              @click="changePay(false)"
            />
            <label class="px-2" for="cash">Cash</label>
          </div>
          <br />
          <div class="container" :class="financePay === true ? 'back' : ''" @click="changePay(true)">
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
              <hr class="ms-3"/>
              <div class="col-md-7 col-xs-11">
                <Dropdown label="Hows your Credit?" :list="credits" />
              </div>
              <br />
              <strong class="p-3">Estimated Monthly Payment</strong>
              <hr class="ms-3"/>
              <div class="row ms-3 me-3">
              <div class="col-md-6 col-xs-12">
                <div class="row">
                  <div class="col-md-5 col-xs-12">
                    <label for="downPay" class="payLabel"> Down Payment</label>
                  </div>
                  <div class="col-md-7 col-xs-12">
                    <input
                      type="text"
                      class="textbox"
                      id="downPay"
                      v-model="slider1Value"
                    />
                  </div>
                </div>
                <VueSlideBar
                  v-model="slider1Value"
                  :min="0"
                  :max="8000"
                  :processStyle="slider.processStyle"
                  :lineHeight="slider.lineHeight"
                  :tooltipStyles="{
                    backgroundColor: 'gray',
                    borderColor: 'black',
                  }"
                >
                </VueSlideBar>
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
                      v-model="slider2Value"
                    />
                  </div>
                </div>
                <VueSlideBar
                  v-model="slider2Value"
                  :data="slider.values"
                  :range="slider.range"
                  :processStyle="slider.processStyle"
                  :lineHeight="slider.lineHeight"
                  :tooltipStyles="{
                    backgroundColor: 'gray',
                    borderColor: 'black',
                  }"
                >
                </VueSlideBar>
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
import VueSlideBar from "vue-slide-bar";

export default {
  name: "Payment",
  components: {
    Dropdown,
    VueSlideBar,
  },
  props:{
    offer:Number
  },
  data() {
    return {
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
      slider: {
        lineHeight: 10,
        processStyle: {
          backgroundColor: "gray",
        },
        values:[
          24,36,48,60,72
        ],
        range:[
          {label:'24'},{label:'36'},{label:'48'},{label:'60'},{label:'72'}
        ]
      },
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
    changePay(choice) {
      this.financePay = choice;
      document.getElementById("cash").checked = !choice;
      document.getElementById("finance").checked = choice;
    },
    handleDisc() {
      this.disclaimer = !this.disclaimer;
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
.message {
  margin-left: auto;
  margin-right: auto;
}
.message-body {
  overflow: hidden;
  transition: 0.3s ease all;
}
.message-header {
  cursor: pointer;
}
.is-closed .message-body {
  max-height: 0;
}
.message-content {
  padding: 20px;
  padding-right: 30px;
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
  color: red;
  border: 1px solid red;
  border-radius: 0.8em;
  padding: auto;
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
.textbox{
  padding: 10px;
  border-radius: 5px;
}
.payLabel{
  padding: 10px 0px;
}
</style>
