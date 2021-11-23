<template>
  <div>
    <article class="message" :class="accordianClasses">
      <div class="message-header" @click="toggleAccordion">
        <div class="row">
          <div class="icon">
            <div class="circle"><i class="far fa-file-alt fa-2x"></i></div>
          </div>
          <div class="icon-text">
            <div :style="{ float: 'left' }">
              <b>Message Dealer</b><i>(Optional)</i>
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
          <h6>Add a short message to the dealer:</h6>
          <textarea
            name="msgToDealer"
            id="msgToDealer"
            v-model="msgToDealer"
            rows="10"
            placeholder="Message to Dealer"
            @input="getData(msgToDealer)"
          ></textarea>
          <p>
            Stay Safe. Read more about
            <a href="#">avoiding scams and protecting your money</a>. By using
            this site, you agree to our <a href="#">Terms of Use</a> & our
            <a href="#">Privacy Policy</a>.
          </p>
        </div>
      </div>
    </article>
  </div>
</template>

<script>
export default {
  name: "Message",
  props: {
    getData: Function,
  },
  data() {
    return {
      msgToDealer: "",
      isOpen: false,
    };
  },
  methods: {
    toggleAccordion() {
      this.isOpen = !this.isOpen;
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
  padding: 10px 20px;
  margin-right: 15px;
}
.fa-file-alt {
  font-size: 1.6em;
  width: 1.6em;
  text-align: center;
  line-height: 1.6em;
  color: darkred;
  padding-top: 10px;
  padding-left: 0px;
  padding-right: 1px;
}
textarea {
  width: 100%;
  border: 1px solid black;
  border-radius: 5px;
}
.angle {
  float: right;
  margin-right: 30px;
}
</style>
