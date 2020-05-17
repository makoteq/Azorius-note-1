<template>
  <div class="wrapper">
    <div class="container">
      <p data-aos="fade-up" style="font-size:3em;" class="title">
        Azorius <span style="color:#ff4b2b">Note</span
        ><b-icon-paperclip></b-icon-paperclip>
      </p>
      <b-container class="h-100" fluid>
        <b-row class="h-100">
          <addComponent v-if="localcheck" />
          <list v-else />
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
import list from "@/components/listComponent.vue";
export default {
  name: "Home",
  components: {
    addComponent,
    getNotes,
    list
  },
  computed: {
    localcheck: function() {
      //localStorage.clear();
      //  localStorage.note1 = "r4";
      if (localStorage.note1) {
        return 0;
      } else {
        return 1;
      }
    }
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
.leftCol {
  min-width: 45vw;
  width: 100%;
  margin: 0;
  padding: 0;
  min-height: 60vh;
  border-radius: 0 10px 0 0;
}
</style>
