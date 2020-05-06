<template>
  <div id="app">
    <router-view />
  </div>
</template>

<style>
@import url("https://fonts.googleapis.com/css?family=Source+Sans+Pro:400,700&display=swap");
body {
  margin: 0;
}
#app {
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
  width: 90%;
  min-height: 60vh;
  padding: 0;
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
