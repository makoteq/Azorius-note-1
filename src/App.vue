<template>
  <div id="app">
    <router-view />
    <footerComponent />
  </div>
</template>
<script>
import footerComponent from "@/components/footerComponent.vue";
export default {
  name: "App",
  components: {
    footerComponent
  }
};
</script>
<style lang="scss">
@import url("https://fonts.googleapis.com/css?family=Source+Sans+Pro:400,700&display=swap");
body {
  margin: 0;
}
#app {
  background: #ebecf0;
  font-family: "Source Sans Pro", sans-serif;
  text-align: center;
  color: black;
  margin: 0;
}

.title {
  font-weight: bold;
  color: black;
  font-size: 1.8em;
  margin: 10px;
}
p {
  color: black;
}

.innerCon {
  display: flex;
  flex-direction: column;
  padding: 0 25px;
  justify-content: center;
  align-items: center;
  width: 90%;
  height: 100%;
  margin: 0 auto;
}
</style>
