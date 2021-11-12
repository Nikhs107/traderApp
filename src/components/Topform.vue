<template>
  <form>
    <div>
      <b>Contact Information</b><br />
      <b class="warning">* </b>Required<br />
      <div class="row my-3">
        <div class="box col-md-6 col-xs-12">
          <input
            type="text"
            class="inputField"
            id="firstname"
            v-model="data.firstname"
          />
          <label for="firstname" class="ms-3">
            First Name<b class="warning">* </b></label
          >
        </div>
        <div class="box col-md-6 col-xs-12">
          <input
            type="text"
            class="inputField"
            id="lastname"
            v-model="data.lastname"
          />
          <label for="lastname" class="ms-3">
            Last Name<b class="warning">* </b></label
          >
        </div>
      </div>
      <div class="row my-3">
        <div class="box col-md-6 col-xs-12">
          <input
            type="email"
            class="inputField"
            id="email"
            v-model="data.email"
          />
          <label for="email" class="ms-3">
            Email<b class="warning">* </b></label
          >
        </div>
        <div class="box col-md-6 col-xs-12">
          <input
            type="text"
            class="inputField"
            id="phonenumber"
            v-model="data.phonenumber"
            @input="numberFormat"
          />
          <label for="phonenumber" class="ms-3"> Phone Number</label>
        </div>
      </div>
      <br /><br />
      <div class="row my-3">
        <div class="col-md-6 col-xs-12">
          <b :style="{ float: 'left' }">My Offer</b>
          <span :style="{ float: 'right' }"
            ><i>Current Asking Price : $8,999</i></span
          >
        </div>
      </div>
      <div class="row my-3">
        <div class="box col-md-6 col-xs-12">
          <input
            type="text"
            class="inputField"
            id="myoffer"
            v-model="data.myoffer"
          />
          <label for="myoffer" class="ms-3">
            Enter Offer<b class="warning">* </b></label
          >
        </div>
      </div>
    </div>
  </form>
</template>
<script>
export default {
  data() {
    return {
      data: {
        firstname: "",
        lastname: "",
        email: "",
        phonenumber: "",
        myoffer: "",
      },
    };
  },
  methods: {
    numberFormat() {
      var x = this.data.phonenumber
        .replace(/\D/g, "")
        .match(/(\d{0,3})(\d{0,3})(\d{0,4})/);
      this.data.phonenumber = !x[2]
        ? x[1]
        : "(" + x[1] + ") " + x[2] + (x[3] ? "-" + x[3] : "");
    },
  },
};
</script>

<style scoped>
label {
  font-size: 15px;
  position: absolute;
  top: 35px;
  left: 25px;
  z-index: 12;
  transition-delay: ease 0.3s;
}
input:focus ~ label {
  transform: translateY(-160%);
  font-size: 10px;
  color: grey;
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
  border-radius: 4px;
  vertical-align: middle;
  box-sizing: border-box;
}
</style>