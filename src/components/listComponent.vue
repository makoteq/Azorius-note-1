<template>
  <b-col class="h-100 leftCol">
    <div class="innerCon">
      <p v-for="item in notes" :key="item.id" class="list">
        <span @click="open(item.code)" class="open">{{ item.code }}</span>
        <span
          v-if="item.code"
          @click="deleteFunc(item.code, item.id)"
          class="delete"
        >
          <b-icon-trash></b-icon-trash
        ></span>
      </p>
    </div>
    <p class="list">
      <router-link to="/add">
        <span v-if="checkNotes" class="add"
          >add <b-icon-plus-square></b-icon-plus-square></span
      ></router-link>
    </p>
  </b-col>
</template>

<script>
import axios from "axios";
export default {
  name: "getComponent",
  data() {
    return {
      notes: [
        { code: "", id: 0 },
        { code: "", id: 1 },
        { code: "", id: 2 }
      ]
    };
  },
  methods: {
    open(code) {
      axios
        .post("/api/getdata", {
          code: code
        })
        .then(response => {
          this.$router.push({
            name: "Note",
            params: { note: response.data[0].note, code: response.data[0].code }
          });
        })
        .catch(error => {
          console.log(error.response);
        });
    },
    deleteFunc(code, id) {
      axios
        .post("/api/delete", {
          code: code
        })
        .then(response => {
          switch (id) {
            case 0:
              localStorage.removeItem("note1");
              break;

            case 1:
              localStorage.removeItem("note2");
              break;

            case 2:
              localStorage.removeItem("note3");
              break;
          }
          console.log(response);
          console.log(this.notes);
          // location.reload();
        })
        .catch(error => {
          console.log(error.response);
        });
    }
  },
  mounted() {
    console.log(this.checkNotes);
    console.log(this.notes);
    if (localStorage.note1) {
      this.$set(this.notes, 0, { code: localStorage.getItem("note1"), id: 0 });
    }
    if (localStorage.note2) {
      this.$set(this.notes, 1, { code: localStorage.getItem("note2"), id: 1 });
    }
    if (localStorage.note3) {
      this.$set(this.notes, 2, { code: localStorage.getItem("note3"), id: 2 });
    }
    console.log(this.notes);
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
  }
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
