<template>
  <div>
    <b class="info">Contact Information</b><br />
    <b class="warning info">* </b>Required<br />
    <div class="row my-3">
      <div class="box col-md-6 col-xs-12">
        <input
          type="text"
          class="inputField"
          id="firstname"
          placeholder=" "
          v-model="data.firstname"
          @blur="handleError('firstname')"
          @input="getData(data)"
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
          placeholder=" "
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
          placeholder=" "
          v-model="data.email"
        />
        <label for="email" class="ms-3"> Email<b class="warning">* </b></label>
      </div>
      <div class="box col-md-6 col-xs-12">
        <input
          type="text"
          class="inputField"
          id="phonenumber"
          placeholder=" "
          v-model="data.phonenumber"
          @input="numberFormat"
        />
        <label for="phonenumber" class="ms-3"> Phone Number</label>
      </div>
    </div>
    <br /><br />
    <div class="row my-3">
      <div class="col-md-6 col-xs-12">
        <div class="row">
          <div class="col-md-6 col-xs-12">
            <b :style="{ float: 'left' }" class="info">My Offer</b>
          </div>
          <div class="col-md-6 col-xs-12">
            <span :style="{ float: 'left' }"
              ><i>Current Asking Price : $8,999</i></span
            >
          </div>
        </div>
      </div>
    </div>
    <div class="row my-3">
      <div class="box col-md-6 col-xs-12">
        <input
          type="text"
          class="inputField"
          id="myoffer"
          placeholder=" "
          v-model="data.myoffer"
        />
        <label for="myoffer" class="ms-3">
          Enter Offer<b class="warning">* </b></label
        >
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    getData: Function,
  },
  data() {
    return {
      data: {
        firstname: "",
        lastname: "",
        email: "",
        phonenumber: "",
        myoffer: "",
      },
      errors: { firstname: "", lastname: "", email: "", myoffer: "" },
    };
  },
  methods: {
    handleError(val) {
      if (val === "firstname" && !this.firstname) {
        this.errors.firstname = "Invalid First Name";
      }
    },
    numberFormat() {
      var x = this.data.phonenumber
        .replace(/\D/g, "")
        .match(/(\d{0,3})(\d{0,3})(\d{0,4})/);
      this.data.phonenumber = !x[2]
        ? x[1]
        : "(" + x[1] + ") " + x[2] + (x[3] ? "-" + x[3] : "");
    },
    currencyFormat() {
      var price = this.data.myoffer;
      let dollar = Intl.NumberFormat("en-US", {
        style: "currency",
        currency: "USD",
        useGrouping: true,
      });
      this.data.myoffer = dollar.format(price);
    },
  },
};
</script>

<style scoped>
label {
  font-size: 15px;
  position: absolute;
  top: 30px;
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
  padding-left: 10px;
  padding-top: -20px;
}
.info {
  padding-left: 22px;
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