<template>
  <div class="wrapper">
    <div data-aos="fade-up" class="container">
      <p style="font-size:3em;" class="title">
        Azorius <span style="color:#ff4b2b">Note</span
        ><b-icon-paperclip></b-icon-paperclip>
      </p>
      <b-container class="h-100" fluid>
        <b-row class="h-100">
          <addComponent />
          <getNotes />
        </b-row>
      </b-container>
    </div>
    <p class="learn">learn how to use</p>
  </div>
</template>

<script>
// @ is an alias to /src
import addComponent from "@/components/addComponent.vue";
import getNotes from "@/components/getnotesComponent.vue";
export default {
  name: "Home",
  components: {
    addComponent,
    getNotes
  }
};
</script>

<style scoped>
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
  min-height: 60vh;
  padding: 0;
}
.learn {
  position: fixed;
  bottom: 0;
  right: 0;
  margin: 20px;
  font-weight: bold;
  cursor: pointer;
}
</style>
