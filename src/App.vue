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
            <TradeIn />
            <hr />
            <Payment :offer="data.myoffer"/>
            <hr />
            <Message />
            <div class="bottom">
              <hr />
              <button class="subBtn" @click="handleSubmit">Submit</button>
            </div>
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
      data: {},
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
      this.data = data;
    },
    handleSubmit() {
      this.submitted = true;
    },
    finished() {
      this.submitted = false;
      this.handleModal();
    },
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
  margin-top: 60px;
}
hr{
  width: 95%;
  text-align: center;
}
.top {
  position: sticky;
  top: 0;
  width: 100%;
  z-index: 100;
  background-color: white;
}
.bottom{
  position: sticky;
  bottom: 0;
  width: 100%;
  z-index: 100;
  text-align: center;
  background-color: white;
  padding-top: 5px;
}
.scrollItems {
  max-height: 600px;
  overflow-y: scroll;
  overflow-x: hidden;
  right: -15px;
  left: 15px;
  top: 60px;
  bottom: 10px;
  position: absolute;
}
.warning {
  color: red;
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
  color: red;
  display: inline-block;
  border-radius: 50px;
  border: 1px solid red;
  padding: 5px;
}
.icon-text {
  margin-left: 10px;
  padding-bottom: 10px;
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
  height: 80%;
  position: relative;
  background-color: white;
  margin: auto;
  padding: 15px;
  text-align: left;
  overflow: hidden;
  border: 1px solid black;
  border-radius: 10px;
}
.subBtn {
  background-color: black;
  color: aliceblue;
  width: 50%;
  border-radius: 5px;
  padding: 10px 0px;
}
</style>
