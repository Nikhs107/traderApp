<template>
  <label class="dropdown" :class="ddBack ? 'back1' : 'back2'">
    <select class="ddInput" required @change="getDDval(ddVal)" v-model="ddVal">
      <option value="" selected disabled hidden></option>
      <option v-for="item in list" :value="item" :key="item">
        {{ item }}
      </option>
    </select>
    <span class="ddLabel">{{ label }}</span>
  </label>
</template>

<script>
export default {
  name: "Dropdown",
  props:{ list:Array, label:String,getDDval:Function,ddBack:Boolean},
  data() {
    return {
      ddVal: "",
    };
  },
};
</script>

<style scoped>
.dropdown {
  position: relative;
  display: block;
  margin-left: -25px;
  margin-right: 25px;
  margin-top: -15px;
}
.dropdown::after {
  content: "\2304";
  position: absolute;
  right: -0.5rem;
  top: 0.6rem;
  transition: 300ms transform 200ms;
}
.dropdown:active::after {
  transform: rotate(-180deg);
}
.ddInput {
  width: 100%;
  padding: 18px 10px;
  padding-bottom: 5px;
  background: white;
  border: 1px solid black;
  margin: 0px 20px;
  border-radius: 5px;
  display: block;
  opacity: 1;
  appearance: none;
  transition-delay: 0ms;
  will-change: color;
  transition: 200ms color linear;
}
.ddInput:invalid {
  transition: 200ms color linear 100ms;
}
.ddInput:valid + .ddLabel,
.ddInput:focus:valid + .ddLabel {
  transform: scale(0.75) translate(-28%, -110%);
  transition: 200ms transform ease-out;
  color: gray;
  padding-left: 15px;
  padding-top: 50px;
  top: -1px;
}
.ddLabel {
  font-size: 15px;
  position: absolute;
  top: 15px;
  bottom: 40px;
  left: 25px;
  z-index: 12;
  transition-delay: ease 0.3s;
}
.back1{
  background: #f0f0f0;
}
.back2{
  background: white;
}
@media (max-width: 750px) {
  .dropdown{
    margin-bottom: 15px;
  }
}
</style>