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
          <div class="container">
            <b>Contact Information</b><br />
            <b class="warning">* </b>Required<br />
            <div class="row my-3">
              <div class="col-md-6 col-xs-12">
                <input
                  class="form-control"
                  type="text"
                  name="firstname"
                  id="firstname"
                  placeholder="First Name"
                />
              </div>
              <div class="col-md-6 col-xs-12">
                <input
                  class="form-control"
                  type="text"
                  name="lastname"
                  id="lastname"
                  placeholder="Last Name"
                />
              </div>
            </div>
            <div class="row my-3">
              <div class="col-md-6 col-xs-12">
                <input
                  class="form-control"
                  type="email"
                  name="email"
                  id="email"
                  placeholder="Email"
                />
              </div>
              <div class="col-md-6 col-xs-12">
                <input
                  class="form-control"
                  type="text"
                  name="phonenumber"
                  id="phonenumber"
                  placeholder="Phone Number"
                />
              </div>
            </div>
            <br><br>
            <div class="row my-3">
              <div class="col-md-6 col-xs-12">
              <b :style="{ float: 'left' }">My Offer</b>
              <span :style="{ float: 'right' }">Current Asking Price : $8,999</span>
              </div>
            </div>
            <div class="row my-3">
              <div class="col-md-6 col-xs-12">
                <input
                  class="form-control"
                  type="text"
                  name="myoffer"
                  id="myoffer"
                  placeholder="Enter Offer"
                />
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Home from "./components/Home.vue";

export default {
  name: "App",
  components: {
    Home,
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
