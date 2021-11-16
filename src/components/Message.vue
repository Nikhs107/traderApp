<template>
  <div>
    <article class="message" :class="accordianClasses">
      <div class="message-header" @click="toggleAccordion">
        <i class="far fa-file-alt fa-2x"></i>
        <span class="icon-text"><b>Message Dealer </b><i>(Optional)</i></span>
        <button
          :style="{
            float: 'right',
            border: 'none',
            background: 'transparent',
          }"
        >
          <i class="fas" :class="isOpen ? 'fa-angle-up' : 'fa-angle-down'"></i>
        </button>
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
          ></textarea>
          <p>Stay Safe. Read more about <a href="#">avoiding scams and protecting your money</a>. By using this site, you agree to our <a href="#">Terms of Use</a> & our <a href="#">Privacy Policy</a>.</p>
        </div>
      </div>
    </article>
  </div>
</template>

<script>
export default {
  name: "Message",
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
.message {
  margin-left: auto;
  margin-right: auto;
}
.message-body {
  overflow: hidden;
  transition: 0.3s ease all;
}
.message-header {
  cursor: pointer;
}
.is-closed .message-body {
  max-height: 0;
}
.message-content {
  padding: 20px;
}
.fa-file-alt {
  font-size: 1.6em;
  width: 1.6em;
  text-align: center;
  line-height: 1.6em;
  color: red;
  border: 1px solid red;
  border-radius: 0.8em;
  padding: auto;
}
textarea{
    width: 100%;
}
</style>
