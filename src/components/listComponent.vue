<template>
  <b-col class="h-100 leftCol">
    <div class="innerCon">
      <p class="list">
        <span class="open">545f</span>
        <span class="delete"> <b-icon-trash></b-icon-trash></span>
      </p>
      <p class="list">
        <span class="open">545f</span>
        <span class="delete"><b-icon-trash></b-icon-trash></span>
      </p>
    </div>
    <p class="list">
      <span class="add">add <b-icon-plus-square></b-icon-plus-square></span>
    </p>
  </b-col>
</template>

<script>
export default {
  name: "getComponent"
};
</script>

<style lang="scss" scoped>
.list {
  font-size: 1.2em;
  font-weight: bold;
  text-align: center;
  padding: 10px;
}
span {
  font-weight: bold;
  cursor: pointer;
  margin-left: 10px;
}
.delete {
  color: red;
  float: right;
  margin-right: 10px;
}
.open {
  cursor: pointer;
  margin-left: 20px;
  font-size: 1.4em;
}
.add {
  cursor: pointer;
  font-size: 1em;
  float: right;
  margin: 20px;
  color: green;
}
</style>
