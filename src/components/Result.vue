<template>
  <div class="container">
    <h2>Trader Data</h2>
    <hr />
    <div class="row header">
      <div class="col-6 border"><b>Property</b></div>
      <div class="col-6 border"><b>Value</b></div>
    </div>
    <div class="row">
      <div class="col-6 border"><b>First Name</b></div>
      <div class="col-6 border">{{ listdata.firstname }}</div>
    </div>
    <div class="row">
      <div class="col-6 border"><b>Last Name</b></div>
      <div class="col-6 border">{{ listdata.lastname }}</div>
    </div>
    <div class="row">
      <div class="col-6 border"><b>Email</b></div>
      <div class="col-6 border">{{ listdata.email }}</div>
    </div>
    <div class="row">
      <div class="col-6 border"><b>Contact</b></div>
      <div class="col-6 border">{{ listdata.phonenumber ? listdata.phonenumber : "---" }}</div>
    </div>
    <div class="row">
      <div class="col-6 border"><b>My Offer</b></div>
      <div class="col-6 border">{{ listdata.myoffer }}</div>
    </div>
    <div class="bottom">
      <hr />
      <button @click="closeModal()" class="subBtn">Close</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Result",
  props: {
    listdata: Object,
    closeModal: Function,
  },
};
</script>
<style scoped>
.container {
  text-align: center;
}
.header {
  background-color: black;
  color: white;
}
</style>
