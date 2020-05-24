<template>
  <b-col class="h-100 rightCol">
    <form v-on:submit.prevent>
      <p style="color:white" class="title">
        Or redeem your code!
      </p>
      <input v-model="code" maxlength="4" placeholder="ID" type="text" /><br />
      <input
        v-model="password"
        placeholder="password"
        type="text"
        v-if="input"
      />
      <span class="password" v-else @click="passwordFunc"
        >Enter password <b-icon-lock-fill></b-icon-lock-fill
      ></span>
      <button @click="getData" class="submit">
        Gimme my notes!
      </button>
    </form>
  </b-col>
</template>

<script>
import Swal from "sweetalert2";
import axios from "axios";
export default {
  name: "getNotesComponent",
  data() {
    return {
      code: "",
      password: "",
      input: false
    };
  },
  methods: {
    getData() {
      axios
        .post("/api/getdata", {
          code: this.code,
          password: this.password
        })
        .then(response => {
          this.$router.push({
            name: "Note",
            params: {
              note: response.data[0].note,
              code: response.data[0].code
            }
          });
        })
        .catch(error => {
          Swal.fire({
            position: "top-end",
            icon: "error",
            title: "Oops...",
            text: "Wrong code or password",
            width: "100",
            showConfirmButton: false,
            timer: 1500
          });
          console.log(error.response);
        });
    },
    passwordFunc() {
      this.input = true;
    }
  }
};
</script>

<style lang="scss" scoped>
.rightCol {
  background-color: #ff4b2b;
  width: 100%;
  margin: 0;
  padding: 0;
  min-height: 60vh;
  border-radius: 0 0 10px 0;
}
input {
  background-color: #f3f3f3;
  border: none;
  line-height: 1.5;
  font-weight: 600;
  padding: 10px;
  border-radius: 5px;
  margin: 10px;
  transition: all 0.4s;
  &:focus {
    outline: 0;
  }
}
.submit {
  border-radius: 5px;
  border: none;
  font-weight: bold;
  outline: none;
  font-size: 12px;
  color: black;
  font-weight: bold;
  padding: 10px 15px;
  margin: 14px;
  letter-spacing: 1px;
  text-transform: uppercase;
  cursor: pointer;
}
.password {
  cursor: pointer;
  font-weight: bold;
  color: white;
}
</style>
