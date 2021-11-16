<template>
  <div class="hello">
    <article class="message" :class="accordianClasses">
      <div class="message-header" @click="toggleAccordion">
        <i class="fas fa-biking fa-2x fontAwesome"></i>
        <span class="icon-text"><b>Have a Trade-in?</b><i>(Optional)</i></span>
        <button
          :style="{
            float: 'right',
            border: 'none',
            background: 'transparent',
          }"
        >
          <i :class="isOpen ? 'fas fa-angle-up' : 'fas fa-angle-down'"></i>
        </button>
      </div>
      <div class="message-body">
        <div class="message-content">
          <div class="col-md-6 col-xs-12">
            <span class="check brd1" :class="!tradeIn ? 'active' : ''" id="no" @click="handleClick('no')"
              >No Trade in</span
            >
            <span class="check brd2" :class="tradeIn ? 'active' : ''" id="yes" @click="handleClick('yes')"
              >Yes, I have a Trade-in</span
            >
          </div>
          <br />
          <div v-show="tradeIn">
            <div class="row my-3">
              <div class="col-md-6 col-xs-12">
                <Dropdown label="Select Year" :list="years" />
              </div>
              <div class="box col-md-6 col-xs-12">
                <input
                  type="text"
                  class="inputField"
                  id="make"
                  placeholder=" "
                  v-model="data.make"
                />
                <label for="make" class="ms-3"> Make</label>
              </div>
            </div>
            <div class="row my-3">
              <div class="box col-md-6 col-xs-12">
                <input
                  type="text"
                  class="inputField"
                  id="model"
                  placeholder=" "
                  v-model="data.model"
                />
                <label for="model" class="ms-3"> Model</label>
              </div>
              <div class="col-md-6 col-xs-12">
                <Dropdown label="Condition" :list="conditions" />
              </div>
            </div>
            <div class="row my-3">
              <div class="box col-md-6 col-xs-12">
                <input
                  type="text"
                  class="inputField"
                  id="mileage"
                  placeholder=" "
                  v-model="data.mileage"
                />
                <label for="mileage" class="ms-3">Estimated Mileage</label>
              </div>
              <div class="box col-md-6 col-xs-12">
                <input
                  type="text"
                  class="inputField"
                  id="vin"
                  placeholder=" "
                  v-model="data.vin"
                />
                <label for="vin" class="ms-3">VIN</label>
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
  name: "TradeIn",
  components: {
    Dropdown,
  },
  data() {
    return {
      data:{make:"",model:""},
      isOpen: false,
      tradeIn: true,
      years: [
        "2005",
        "2006",
        "2007",
        "2008",
        "2009",
        "2010",
        "2011",
        "2012",
        "2013",
        "2014",
        "2015",
        "2016",
        "2017",
        "2018",
        "2019",
        "2020",
        "2021",
      ],
      conditions: ["Excellent", "Good", "Fair", "Poor"],
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
  padding: 30px 0px;
}
.check,
.active {
  width: 30%;
  cursor: pointer;
  margin-top: 15px;
  margin-bottom: 15px;
  padding: 15px;
  border: 1px solid black;
}
.brd2{
  border-radius: 0px 5px 5px 0px;
}
.brd1{
  border-radius: 5px 0px 0px 5px;
}
.check {
  background: white;
}
.active {
  background: #b5251920;
  border: 2px solid #b52519;
}
label {
  font-size: 15px;
  position: absolute;
  top: 30px;
  bottom: 40px;
  left: 25px;
  z-index: 12;
  transition-delay: ease 0.3s;
}
input:focus ~ label, input:not(:placeholder-shown) ~ label {
  transform: translate(-20%, -160%);
  font-size: 10px;
  color: grey;
  padding-left: 10px;
  padding-top: -20px;
}
.box {
  display: inline-block;
  position: relative;
  width: 45%;
}
.inputField {
  width: 100%;
  padding: 18px 20px;
  position: relative;
  font-size: 15px;
  margin: 10px 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
}
</style>
