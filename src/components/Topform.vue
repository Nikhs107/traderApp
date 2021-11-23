<template>
  <div>
    <b class="info">Contact Information</b><br />
    <b class="warning info">* </b>Required<br /><br />
    <div class="row me-5">
      <div class="box col-sm-12 col-lg-6 col-md-6 col-xs-12">
        <input
          type="text"
          class="inputField"
          id="firstname"
          placeholder=" "
          v-model="data.firstname"
          @input="getData(data)"
          @blur="handleError('firstname')"
        />
        <label for="firstname" class="ms-3">
          First Name<b class="warning">* </b></label
        >
        <b v-if="errors.firstname" class="warning err"
          ><i class="fa fa-exclamation-circle"></i>{{ errors.firstname }}</b
        ><b v-else>&nbsp;</b>
      </div>
      <div class="box col-sm-12 col-lg-6 col-md-6 col-xs-12">
        <input
          type="text"
          class="inputField"
          id="lastname"
          placeholder=" "
          v-model="data.lastname"
          @input="getData(data)"
          @blur="handleError('lastname')"
        />
        <label for="lastname" class="ms-3">
          Last Name<b class="warning">* </b></label
        >
        <b v-if="errors.lastname" class="warning err"
          ><i class="fa fa-exclamation-circle"></i>{{ errors.lastname }}</b
        ><b v-else>&nbsp;</b>
      </div>
    </div>
    <div class="row me-5">
      <div class="box col-sm-12 col-lg-6 col-md-6 col-xs-12">
        <input
          type="email"
          class="inputField"
          id="email"
          placeholder=" "
          v-model="data.email"
          @input="getData(data)"
          @blur="handleError('email')"
        />
        <label for="email" class="ms-3"> Email<b class="warning">* </b></label>
        <b v-if="errors.email" class="warning err"
          ><i class="fa fa-exclamation-circle"></i>{{ errors.email }}</b
        ><b v-else>&nbsp;</b>
      </div>
      <div class="box col-sm-12 col-lg-6 col-md-6 col-xs-12">
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
    <br />
    <div class="row">
      <div class="col-sm-12 col-lg-6 col-md-6 col-xs-12">
        <div class="row">
          <div class="col-sm-12 col-lg-6 col-md-6 col-xs-12">
            <b class="info">My Offer</b>
          </div>
          <div class="col-sm-12 col-lg-6 col-md-6 col-xs-12">
            <span class="respI"><i>Current Asking Price : $8,999</i></span>
          </div>
        </div>
      </div>
    </div>
    <div class="row me-5">
      <div class="box col-sm-12 col-lg-6 col-md-6 col-xs-12">
        <input
          type="number"
          class="inputField"
          id="myoffer"
          placeholder=" "
          v-model="data.myoffer"
          @input="getData(data)"
          @blur="handleError('myoffer')"
        />
        <label for="myoffer" class="ms-3">
          Enter Offer<b class="warning">* </b></label
        >
        <b v-if="errors.myoffer" class="warning err"
          ><i class="fa fa-exclamation-circle"></i>{{ errors.myoffer }}</b
        ><b v-else>&nbsp;</b>
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
        myoffer: 0,
      },
      errors: { firstname: "", lastname: "", email: "", myoffer: "" },
    };
  },
  methods: {
    handleError(val) {
      if (val === "firstname") {
        if(!this.data.firstname)
        this.errors.firstname = " Invalid First Name";
        else this.errors.firstname = "";
      }
      if (val === "lastname") {
        if(!this.data.lastname)
        this.errors.lastname = " Invalid Last Name";
        else this.errors.lastname = "";
      }
      if (val === "email") {
        if(!this.data.email)
        this.errors.email = " Invalid Email";
        else if(!this.data.email.includes("@")||!this.data.email.includes("."))
        this.errors.email = " Invalid Email";
        else this.errors.email = "";
      }
      if (val === "myoffer") {
        if (this.data.myoffer <= 7500) {
          this.errors.myoffer =
            " Your offer is too low. Please improve your offer.";
        } else this.errors.myoffer = "";
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
  },
};
</script>

<style scoped>
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
  padding-left: 15px;
  padding-top: 50px;
  top: 33px;
}
.info {
  padding-left: 22px;
}
.box {
  position: relative;
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
.err {
  padding-left: 20px;
  font-size: 10px;
}
</style>