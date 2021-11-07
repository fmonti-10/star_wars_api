<template>
  <div id="app">
    <div class="container">
      <img class="logo" src="src\assets\star_wars_logo.png" />
      <h4 class="text">Listado de Personajes</h4>
      <div clas="list" v-for="(p, index) in people" :key="index">
        <p class="list_name" @click="showPerson(p)">
          {{ p.name }}
        </p>
        <div
          class="list_data"
          v-if="person_data.show && p.name == person_data.name"
        >
          <p v-if="p.height != 'n/a'">Altura: {{ person_data.height }}cm</p>
          <p v-if="p.hair_color != 'n/a' && p.hair_color != 'none'">
            Color de pelo: {{ person_data.hair_color }}
          </p>
          <p class="gender" v-if="p.gender != 'n/a'">
            Genero: {{ person_data.gender }}
          </p>
        </div>
      </div>
      <div class="buttons">
        <div class="reset">
          <button class="reset_button" @click="reset()">
            Resetear ordenación
          </button>
        </div>
        <div class="button">
          <button class="button_name" @click="sortByName()">
            Ordenar por nombre
          </button>
          <button class="button_height" @click="sortByHeight()">
            Ordenar por altura
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      peopleDefault: null,
      people: null,
      person_data: {},
      show: false,
    };
  },

  methods: {
    sortByName() {
      this.people.sort(function (a, b) {
        var nameA = a.name;
        var nameB = b.name;
        return nameA < nameB ? -1 : nameA > nameB ? 1 : 0;
      });
    },

    sortByHeight() {
      this.people.sort(function (a, b) {
        var heightA = parseInt(a.height);
        var heightB = parseInt(b.height);
        return heightA < heightB ? -1 : heightA > heightB ? 1 : 0;
      });
    },
    showPerson(p) {
      this.person_data = p;
      if (this.person_data.show == undefined) {
        this.person_data.show = true;
      }
    },
    reset() {
      this.people = [].concat(...this.peopleDefault);
    },
  },

  mounted() {
    const axios = require("axios").default;
    axios
      .get("https://swapi.dev/api/people/")
      .then((response) => (this.peopleDefault = response.data.results));
    axios
      .get("https://swapi.dev/api/people/")
      .then((response) => (this.people = response.data.results));
  },
};
</script>

<style lang="scss">
body {
  margin: 0;
}
#app {
  overflow-y: auto;
  height: 100%;
  position: fixed;
  width: 100%;
  z-index: -100;
  background: url("../src/assets/star-wars-background.png") no-repeat center
    center fixed;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;
  background-color: black;
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: flex;
  justify-content: center;
  align-items: center;
  .container {
    box-shadow: 0 0 10px #4cb1fa;
    width: 70%;
    height: fit-content;
    background-color: #141414;
    padding: 40px 0;
    display: flex;
    flex-flow: column;
    align-items: center;
    .logo {
      width: 40%;
    }
    .text {
      font-size: 16px;
      margin-top: 1rem;
      margin-bottom: 0;
      color: #4cb1fa;
    }
    .list {
      display: flex;
      flex-flow: column;
      align-items: center;
      width: max-content;
      &_name {
        font-size: 10px;
        color: #cfcfcf;
        margin-bottom: 3px;
      }
      &_name:hover {
        color: white;
        text-decoration: underline;
        cursor: pointer;
      }
      &_data {
        font-size: 10px;
        color: #4cb1fa;
      }
    }
    .buttons {
      display: flex;
      justify-content: center;
      width: 100%;
      margin-top: 2%;
    }
    .button {
      align-self: flex-end;
      width: 100%;
      display: flex;
      flex-flow: row;
      justify-content: flex-end;
      margin-right: 5%;
      &_name {
        margin-right: 5px;
        background-color: #141414;
        border-color: #4cb1fa;
        border-radius: 4px;
        color: #cfcfcf;
      }
      &_name:hover {
        background-color: #4cb1fa;
        border-color: #4cb1fa;
        color: #141414;
        cursor: pointer;
      }
      &_height {
        background-color: #141414;
        border-color: #e51a4c;
        border-radius: 4px;
        color: #cfcfcf;
      }
      &_height:hover {
        background-color: #e51a4c;
        border-color: #e51a4c;
        color: #141414;
        cursor: pointer;
      }
      &_height,
      &_name {
        min-height: 25px;
        font-size: 10px;
      }
    }
    .reset {
      align-self: flex-end;
      margin-left: 5%;
      .reset_button {
        background-color: #141414;
        border-color: #ffe81f;
        border-radius: 4px;
        color: #cfcfcf;
        min-height: 25px;
        font-size: 10px;
        width: 140%;
      }
      .reset_button:hover {
        background-color: #ffe81f;
        border-color: #ffe81f;
        color: #141414;
        cursor: pointer;
      }
    }
  }
}
@media (min-width: 1280px) {
  #app {
    .container {
      box-shadow: 0 0 10px #4cb1fa;
      width: 70%;
      height: fit-content;
      background-color: #141414;
      padding: 40px 0;
      display: flex;
      flex-flow: column;
      align-items: center;
      .logo {
        width: 40%;
      }
      .text {
        font-size: 1rem;
        margin-top: 1rem;
        margin-bottom: 0;
        color: #4cb1fa;
      }
      .list {
        display: flex;
        flex-flow: column;
        align-items: center;
        width: max-content;
        &_name {
          font-size: 12px;
          color: #cfcfcf;
          margin-bottom: 3px;
        }
        &_name:hover {
          color: white;
          text-decoration: underline;
          cursor: pointer;
        }
        &_data {
          font-size: 12px;
          color: #4cb1fa;
          .gender {
            margin-bottom: 0;
          }
        }
      }

      .button {
        width: 100%;
        display: flex;
        flex-flow: row;
        justify-content: flex-end;
        margin-right: 5%;
        margin-top: 2%;

        &_name {
          margin-right: 5px;
          background-color: #141414;
          border-color: #4cb1fa;
          border-radius: 4px;
          color: #cfcfcf;
        }
        &_name:hover {
          background-color: #4cb1fa;
          border-color: #4cb1fa;
          color: #141414;
          cursor: pointer;
        }
        &_height {
          background-color: #141414;
          border-color: #e51a4c;
          border-radius: 4px;
          color: #cfcfcf;
        }
        &_height:hover {
          background-color: #e51a4c;
          border-color: #e51a4c;
          color: #141414;
          cursor: pointer;
        }
        &_height,
        &_name {
          min-height: 30px;
        }
      }
    }
  }
}
</style>
