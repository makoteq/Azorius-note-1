<template>
  <div class="wrapper">
    <p @click="goBack" class="goBack">go back</p>
    <div class="container">
      <div class="innerCon" style="padding:0">
        <p data-aos="fade-up" style="font-size:2.5em" class="title">
          Note <span>{{ code }}</span>
        </p>
        <p>{{ note }}</p>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "Note",
  data() {
    return {
      note: this.$route.params.note,
      code: this.$route.params.code
    };
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
