<template>
  <article class="message" :class="accordianClasses">
    <div class="message-header" @click="toggleAccordion">
      <div class="row">
        <div class="icon">
          <div class="circle">
            <i class="fas fa-biking fa-2x fontAwesome"></i>
          </div>
        </div>
        <div class="icon-text">
          <div :style="{ float: 'left' }">
            <b>Have a Trade-in?</b><i>(Optional)</i>
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
        <div class="head col-md-6 col-sm-12 col-xs-12 col-lg-6">
          <button
            class="check brd1"
            :class="!tradeIn ? 'active' : ''"
            id="no"
            @click="handleClick('no')"
          >
            No Trade in
          </button>
          <button
            class="check brd2"
            :class="tradeIn ? 'active' : ''"
            id="yes"
            @click="handleClick('yes')"
          >
            Yes, I have a Trade-in
          </button>
        </div>
        <br />
        <div v-show="tradeIn">
          <div class="row">
            <div class="box col-md-6 col-sm-12 col-xs-12 col-lg-6">
              <Dropdown
                label="Select Year"
                :list="years"
                :getDDval="assignYear"
                :ddBack="false"
              />
            </div>
            <div class="box col-md-6 col-sm-12 col-xs-12 col-lg-6">
              <input
                type="text"
                class="inputField"
                id="make"
                placeholder=" "
                v-model="data.make"
                @input="getData"
              />
              <label for="make" class="ms-3"> Make</label>
            </div>
          </div>
          <div class="row">
            <div class="box col-md-6 col-sm-12 col-xs-12 col-lg-6">
              <input
                type="text"
                class="inputField"
                id="model"
                placeholder=" "
                v-model="data.model"
                @input="getData"
              />
              <label for="model" class="ms-3"> Model</label>
            </div>
            <div class="box col-md-6 col-sm-12 col-xs-12 col-lg-6">
              <Dropdown
                label="Condition"
                :list="conditions"
                :getDDval="assignCon"
                :ddBack="false"
              />
            </div>
          </div>
          <div class="row">
            <div class="box col-md-6 col-sm-12 col-xs-12 col-lg-6">
              <input
                type="text"
                class="inputField"
                id="mileage"
                placeholder=" "
                v-model="data.mileage"
                @input="getData"
              />
              <label for="mileage" class="ms-4">Estimated Mileage</label>
            </div>
            <div class="box col-md-6 col-sm-12 col-xs-12 col-lg-6">
              <input
                type="text"
                class="inputField"
                id="vin"
                placeholder=" "
                v-model="data.vin"
                @input="getData"
              />
              <label for="vin" class="ms-3">VIN</label>
            </div>
          </div>
        </div>
      </div>
    </div>
  </article>
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
      data: {
        tradeIn: true,
        make: "",
        model: "",
        year: "",
        condition: "",
        mileage: "",
        vin: "",
      },
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
        this.data.tradeIn = false;
        this.getData();
      } else {
        document.getElementById(id).className = "active";
        document.getElementById("no").className = "check";
        this.data.tradeIn = true;
        this.getData();
      }
    },
    getData() {
      this.$emit("tradeData", this.data);
    },
    assignYear(val) {
      this.data.year = val;
    },
    assignCon(val) {
      this.data.condition = val;
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
  margin-right: 55px;
}
.check,
.active {
  cursor: pointer;
  margin-top: 15px;
  margin-bottom: 15px;
  padding: 15px;
  border: 1px solid black;
}
.brd2 {
  border-radius: 0px 5px 5px 0px;
}
.brd1 {
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
  top: 15px;
  bottom: 40px;
  left: 25px;
  z-index: 12;
  transition-delay: ease 0.3s;
}
input:focus ~ label,
input:not(:placeholder-shown) ~ label {
  transform: translate(-20%, -160%);
  font-size: 10px;
  color: grey;
  padding-left: 11px;
  padding-top: 50px;
  top: 33px;
}
.box {
  position: relative;
  margin: 10px 0px;
}
.inputField {
  width: 100%;
  padding: 18px 10px;
  padding-bottom: 5px;
  position: relative;
  font-size: 15px;
  margin: 0px 20px;
  border: 1px solid black;
  border-radius: 5px;
}
.head {
  margin-left: 20px;
}
@media (max-width: 750px) {
  .box{
    margin: 15px 0px;
  }
}
</style>
