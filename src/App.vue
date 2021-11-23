<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <Home msg="Welcome to Your Trader App" />
    <div class="flex-container">
      <button class="btn btn-primary" @click="handleModal">Enter</button>
      <div class="modal" ref="mymodal">
        <div class="modal-content">
          <div class="top">
            <h3 :style="{ float: 'left' }">Make An Offer</h3>
            <button
              :style="{
                float: 'right',
                border: 'none',
                background: 'transparent',
              }"
              @click="handleModal"
            >
              <i class="fas fa-times fa-2x"></i>
            </button>
          </div>
          <div class="scrollItems" v-show="!submitted">
            <Topform :getData="getTopForm" />
            <hr />
            <TradeIn @tradeData="getTradeData" />
            <hr />
            <Payment @payData="getPayData" />
            <hr />
            <Message :getData="getMsg" />
          </div>
          <div class="bottom" v-show="!submitted">
            <hr />
            <button class="subBtn" @click="handleSubmit">Submit</button>
          </div>
          <div v-show="submitted">
            <Result :listdata="data" :closeModal="finished" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Home from "./components/Home.vue";
import Topform from "./components/Topform.vue";
import TradeIn from "./components/TradeIn.vue";
import Payment from "./components/Payment.vue";
import Message from "./components/Message.vue";
import Result from "./components/Result.vue";

export default {
  name: "App",
  components: {
    Home,
    Topform,
    TradeIn,
    Payment,
    Message,
    Result,
  },
  data() {
    return {
      data: {
        Topform: {},
        TradeIn: {},
        PayData: {},
        msg: "",
      },
      submitted: false,
    };
  },
  methods: {
    handleModal() {
      let view = this.$refs.mymodal.style.display;
      if (!view) {
        this.$refs.mymodal.style.display = "block";
      } else {
        this.$refs.mymodal.style.display = view === "none" ? "block" : "none";
      }
    },
    getTopForm(data) {
      this.data.Topform = data;
    },
    getTradeData(data) {
      //this.data = Object.assign(this.data, data);
      this.data.TradeIn = data;
    },
    getPayData(data) {
      //this.data = Object.assign(this.data, data);
      this.data.PayData = data;
    },
    getMsg(msg) {
      this.data.msg = msg;
    },
    handleSubmit() {
      this.submitted = true;
      console.log("Submit", this.data);
    },
    finished() {
      this.submitted = false;
      this.handleModal();
    },
  },
  mounted() {
    console.log("App", this.data);
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
hr {
  width: 98%;
}
.top {
  position: sticky;
  top: 0;
  width: 100%;
  z-index: 100;
  background-color: white;
}
.bottom {
  position: absolute;
  bottom: 0px;
  width: 100%;
  text-align: center;
  background-color: white;
  padding-top: 1px;
  padding-bottom: 10px;
  padding-left: 15px;
  right: 2px;
  z-index: 100;
  border-radius: 15px;
}
.scrollItems {
  max-height: 500px;
  overflow-y: scroll;
  display: block;
  overflow-x: hidden;
  right: -15px;
  left: 15px;
  top: 60px;
  bottom: 10px;
  position: absolute;
}
.warning {
  color: darkred;
}
.flex-container {
  display: flex;
  justify-content: center;
  align-items: center;
}
.btn {
  cursor: pointer;
}
.fontAwesome {
  color: darkred;
  padding: 6px;
  padding-left: 5px;
  line-height: 40px;
}
.circle {
  border-radius: 50%;
  width: 40px;
  height: 40px;
  border: 1px solid darkred;
}
.modal {
  position: fixed;
  z-index: 1;
  padding-top: 100px;
  left: 0;
  top: 0;
  background-color: rgba(0, 0, 0, 0.4);
}
.modal-content {
  max-width: 50%;
  height: 81%;
  background-color: white;
  margin: auto;
  padding: 15px;
  padding-bottom: 0px !important;
  text-align: left;
  overflow: hidden;
  border-radius: 15px !important;
}
.message {
  margin: auto;
}
.message-body {
  overflow: hidden;
  transition: 0.3s ease all;
}
.message-header {
  cursor: pointer;
  margin-right: 55px;
  margin-left: 15px;
}
.is-closed .message-body {
  max-height: 0;
}
.subBtn {
  background-color: black;
  color: aliceblue;
  width: 50%;
  border-radius: 5px;
  padding: 10px 0px;
}
.icon-text {
  padding: 10px 0px;
  margin-left: 50px;
}
.icon {
  float: left;
  width: 50px;
  position: absolute;
}
.angle {
  float: right;
  margin-right: 30px;
}
.check {
  width: 50%;
}
@media (max-width: 750px) {
  .modal-content {
    width: 100%;
    max-width: 100%;
    height: 100%;
    border-radius: 0px !important;
  }
  .modal {
    padding-top: 0px;
  }
  .scrollItems {
    max-height: 650px;
    padding-right: 12px;
  }
  .respI {
    margin-left: 20px;
  }
  .check {
    width: 100%;
  }
}
@media (max-width: 1000px) {
  .check {
    width: 100%;
  }
}
@media (max-height: 1367px) {
  @media (min-height: 1023px) {
    .modal-content {
      max-height: 650px;
    }
  }
}
@media (max-height: 732px) {
  .scrollItems {
    max-height: 480px;
  }
}
@media (min-height: 731px) {
  @media (max-height: 736px) {
  .scrollItems {
    max-height: 570px;
  }
  }
}
@media (height: 568px) {
  .scrollItems {
    max-height: 400px;
  }
}
</style>
