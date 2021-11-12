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
          <div class="scrollItems">
            <Topform />
            <hr />
            <TradeIn />
            <hr />
            <Payment />
            <hr />
            <Message />
            <hr />
            <button class="btn btn-dark" type="submit">Submit</button>
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

export default {
  name: "App",
  components: {
    Home,
    Topform,
    TradeIn,
    Payment,
    Message,
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
.top {
  position: sticky;
  top: 0;
  width: 100%;
  z-index: 100;
}
.scrollItems {
  max-height: 600px;
  overflow-y: auto;
  overflow-x: hidden;
}
.col-1 {
  text-align: right;
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
  display: none;
  position: fixed;
  z-index: 1;
  padding-top: 100px;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  background-color: rgb(0, 0, 0);
  background-color: rgba(0, 0, 0, 0.4);
}
.modal-content {
  max-width: 50%;
  position: relative;
  background-color: white;
  margin: auto;
  padding: 15px;
  text-align: left;
  border: 1px solid #888;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  animation-name: animatetop;
  animation-duration: 0.4s;
}
</style>
