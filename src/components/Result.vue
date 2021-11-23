<template>
  <div class="container" @load="showData">
    <h2>Trader Data</h2>
    <hr />
    <div class="scrollRst">
    <div class="row header">
      <div class="col-6 border"><b>Property</b></div>
      <div class="col-6 border"><b>Value</b></div>
    </div>
    <div class="row">
      <div class="col-6 border"><b>First Name</b></div>
      <div class="col-6 border">{{ listdata.Topform.firstname }}</div>
    </div>
    <div class="row">
      <div class="col-6 border"><b>Last Name</b></div>
      <div class="col-6 border">{{ listdata.Topform.lastname }}</div>
    </div>
    <div class="row">
      <div class="col-6 border"><b>Email</b></div>
      <div class="col-6 border">{{ listdata.Topform.email }}</div>
    </div>
    <div class="row">
      <div class="col-6 border"><b>Contact</b></div>
      <div class="col-6 border">{{ listdata.Topform.phonenumber || "---" }}</div>
    </div>
    <div class="row">
      <div class="col-6 border"><b>My Offer</b></div>
      <div class="col-6 border">{{ listdata.Topform.myoffer }}</div>
    </div>
    <div class="row">
      <div class="col-6 border"><b>TradeIn</b></div>
      <div class="col-6 border">{{ listdata.TradeIn.tradeIn}}</div>
    </div>
    <div class="row">
      <div class="col-6 border"><b>TradeIn: Year</b></div>
      <div class="col-6 border">{{ listdata.TradeIn.year || "---" }}</div>
    </div>
    <div class="row">
      <div class="col-6 border"><b>TradeIn: Make</b></div>
      <div class="col-6 border">{{ listdata.TradeIn.make || "---" }}</div>
    </div>
    <div class="row">
      <div class="col-6 border"><b>TradeIn: Model</b></div>
      <div class="col-6 border">{{ listdata.TradeIn.model || "---" }}</div>
    </div>
    <div class="row">
      <div class="col-6 border"><b>TradeIn: Condition</b></div>
      <div class="col-6 border">{{ listdata.TradeIn.condition || "---" }}</div>
    </div>
    <div class="row">
      <div class="col-6 border"><b>TradeIn: Mileage</b></div>
      <div class="col-6 border">{{ listdata.TradeIn.mileage || "---" }}</div>
    </div>
    <div class="row">
      <div class="col-6 border"><b>TradeIn: VIN</b></div>
      <div class="col-6 border">{{ listdata.TradeIn.vin || "---" }}</div>
    </div>
    <div class="row">
      <div class="col-6 border"><b>Cash Payment</b></div>
      <div class="col-6 border">{{ listdata.PayData.cash }}</div>
    </div>
    <div class="row">
      <div class="col-6 border"><b>Credits</b></div>
      <div class="col-6 border">{{ listdata.PayData.credits || "---" }}</div>
    </div>
    <div class="row">
      <div class="col-6 border"><b>Down Payment</b></div>
      <div class="col-6 border">{{ listdata.PayData.downPay || "---" }}</div>
    </div>
    <div class="row">
      <div class="col-6 border"><b>Terms (months)</b></div>
      <div class="col-6 border">{{ listdata.PayData.terms || "---" }}</div>
    </div>
    <div class="row">
      <div class="col-6 border"><b>Message to Dealer</b></div>
      <div class="col-6 border">{{ listdata.msg || "---" }}</div>
    </div></div>
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
  methods:{
    showData(){
      console.log('result',this.listdata);
    }
  },
  mounted(){
    console.log(this.listdata);
  }
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
.scrollRst {
  max-height: 440px;
  overflow-y: scroll;
  overflow-x: hidden;
  right: -15px;
  left: 15px;
  top: 60px;
}
@media(max-width:750px){
  .scrollRst{
  padding-left: 10px;
  }
}
</style>
