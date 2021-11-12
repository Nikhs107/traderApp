<template>
  <select v-model="selected" class="dropDown">
    <option disabled value="">{{ label }}</option>
    <option :key="item" v-for="item in list" :value="item">{{ item }}</option>
  </select>
</template>

<script>
export default {
  name: "Dropdown",
  data() {
    return {
      selected: "",
    };
  },
  props: ["list", "label"],
};
</script>

<style scoped>
.dropDown {
  width: 90%;
  padding: 18px 20px;
  font-size: 15px;
  background: white;
  margin: 8px 15px;
  border-radius: 4px;
  box-sizing: border-box;
}
</style>