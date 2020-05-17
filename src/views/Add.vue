<template>
  <div class="wrapper">
    <p @click="goBack" class="goBack">go back</p>
    <addComponent />
  </div>
</template>
<script>
import addComponent from "@/components/addComponent.vue";
export default {
  name: "Note",
  components: {
    addComponent
  },
  methods: {
    goBack() {
      this.$router.push({
        name: "Home"
      });
    }
  }
};
</script>
<style lang="scss" scoped>
.wrapper {
  width: 100%;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: #ebecf0;
}
.container {
  border-radius: 10px;
  box-shadow: -5px -5px 10px #fff, 5px 5px 10px #babebc;
  width: 85%;
  min-height: 60vh;
  padding: 0;
}
.goBack {
  position: absolute;
  top: 0;
  margin: 20px;
  left: 0;
  cursor: pointer;
  color: black;
  font-weight: bold;
}
span {
  color: #ff4b2b;
}
</style>
