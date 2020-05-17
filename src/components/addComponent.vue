<template>
  <b-col class="h-100 leftCol">
    <form v-on:submit.prevent class="innerCon">
      <p class="title">Note!</p>
      <textarea
        @input="replace"
        v-model="note"
        rows="10"
        maxlength="2000"
      ></textarea>
      <div>
        <input v-model="interactive" type="checkbox" />
        <span>
          Use interactive tags
          <b-icon-question-diamond></b-icon-question-diamond
        ></span>
      </div>

      <input
        v-model="password"
        placeholder="password"
        type="text"
        v-if="input"
      />
      <span class="password" v-else @click="passwordFunc"
        >Create password <b-icon-lock-fill></b-icon-lock-fill
      ></span>
      <button @click="send" class="submit">Submit</button>
    </form>
    <!-- <b-modal ok-only ok-variant="outline-warning" ok-title="OK" id="modal-1">
      <p>
        Your code is<span id="code" class="title">{{ code }}</span>
      </p>
      <span style="cursor:pointer" @click="getNote">Show me my note!</span>
    </b-modal>-->
  </b-col>
</template>

<script>
import debounce from "lodash.debounce";
import axios from "axios";
import Swal from "sweetalert2";
export default {
  name: "addComponent",
  data() {
    return {
      input: false,
      note: "",
      notes: {
        one: {
          time: 0,
          status: ""
        },
        two: { time: 0, status: "" },
        three: { time: 0, status: "" }
      },
      password: "",
      interactive: 1,
      code: ""
    };
  },
  computed: {
    checkNotes() {
      let count = 0;
      if (localStorage.note1) count++;
      if (localStorage.note2) count++;
      if (localStorage.note3) count++;
      console.log(count);
      if (count == 3) return false;
      else return true;
    }
  },
  methods: {
    send() {
      if (this.checkNotes == false) {
        Swal.fire({
          position: "top-end",
          icon: "error",
          title: "Oops...",
          text: "You can't create more then 3 notes.",
          width: "100",
          showConfirmButton: false,
          timer: 1500
        });
      } else {
        axios
          .post("/api/insert", {
            note: this.note,
            password: this.password
          })
          .then(response => {
            this.code = response.data.code;
            if (!localStorage.note1) {
              localStorage.note1 = response.data.code;
            } else if (!localStorage.note2) {
              localStorage.note2 = response.data.code;
            } else {
              localStorage.note3 = response.data.code;
            }
            this.$router.push({
              name: "Note",
              params: { note: this.note, code: this.code }
            });
          })
          .catch(error => {
            console.log(error.response);
          });
      }
    },
    getNote() {
      /*reset form*/
      this.note = "";
      this.interactive = 1;
      this.input = false;
    },
    replace: debounce(function() {
      const today = new Date();
      const tomorrow = new Date(today);
      tomorrow.setDate(tomorrow.getDate() + 1);
      const yesterday = new Date(today);
      yesterday.setDate(yesterday.getDate() - 1);
      var note = this.note;
      var interactive = this.interactive;
      var tags = [
        "!link",
        "!header",
        "!bold",
        "!italic",
        "!today",
        "!tommorow",
        "!yesterday",
        "!time",
        "!lorem",
        "!tip",
        "!random",
        "!dice",
        "!joke",
        "!lanyface"
      ];
      tags.forEach(function(item) {
        if (note.includes(item) && interactive) {
          switch (item) {
            case "!link":
              note = note.replace(item, "[mysite](https://mysite.com)");
              break;
            case "!header":
              note = note.replace(item, "###### This is big header");
              break;
            case "!italic":
              note = note.replace(item, "* *");
              break;
            case "!lanyface":
              note = note.replace(item, "( ͡° ͜ʖ ͡°)");
              break;
            case "!bold":
              note = note.replace(item, "** **");
              break;
            case "!today":
              note = note.replace(item, today.toLocaleString());
              break;
            case "!tommorow":
              note = note.replace(item, tomorrow.toLocaleString());
              break;
            case "!yesterday":
              note = note.replace(item, yesterday.toLocaleString());
              break;
            case "!time":
              note = note.replace(
                item,
                today.getHours() + ":" + today.getMinutes()
              );
              break;
            case "!lorem":
              note = note.replace(
                item,
                "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
              );
              break;
            case "!tip":
              note = note.replace(item, "Try to use .md tags!");
              break;
            case "!random":
              note = note.replace(item, Math.floor(Math.random() * 10));
              break;
            case "!dice":
              note = note.replace(item, Math.floor(Math.random() * 7));
              break;
            case "!joke":
              note = note.replace(
                item,
                "What's red, and smells like blue paint? Red paint."
              );

              break;
          }
        }
      });

      this.note = note;
    }, 500),
    passwordFunc() {
      this.input = true;
    }
  }
};
</script>

<style lang="scss" scoped>
span {
  color: black;
  font-weight: bold;
}
.password {
  cursor: pointer;
}
input,
textarea {
  background-color: #f3f3f3;
  border: none;
  line-height: 1.5;
  font-weight: 600;
  padding: 10px;
  border-radius: 5px;
  margin: 10px;
  max-width: 40vw;
  transition: all 0.4s;
  &:focus {
    outline: 0;
  }
}
textarea {
  width: 90%;
  box-shadow: -5px -5px 10px #fff, 5px 5px 10px #babebc;
}
.submit {
  border-radius: 20px;
  border: none;
  outline: none;
  font-size: 12px;
  font-weight: bold;
  padding: 15px 45px;
  margin: 14px;
  letter-spacing: 1px;
  text-transform: uppercase;
  cursor: pointer;
  transition: transform 80ms ease-in;
  box-shadow: -5px -5px 10px #fff, 5px 5px 8px #babebc;
  &:active {
    box-shadow: inset 1px 1px 2px #babebc, inset -1px -1px 2px #fff;
  }
}
.title {
  font-weight: bold;
  color: black;
  font-size: 1.8em;
  margin: 10px;
}
</style>
