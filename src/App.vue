<template>
  <h1>{{ text }}</h1>
  <!-- Esta Variable Algo esta creada en el mixin -->
  <h2>{{ algo }}</h2>
  <button @click="show = !show">Menu</button>
  <!-- Usando transiciones con vue -->
  <transition name="fade">
    <menu-header v-show="show" />
  </transition>
  <div>
    <modal-vue />
  </div>
  <img alt="Vue logo" src="./assets/logo.png" />
  <component :is="componente"> </component>
  <user-repositories :user="'Carlos'"></user-repositories>
  <home-composition year-birth="1980" month-birth="Marzo"></home-composition>
</template>

<script>
// cargando un componente de forma normal
// import HelloWorld from "./components/HelloWorld.vue";

import base from "@/mixins/base";
import MenuHeader from "./components/MenuHeader.vue";
import ModalVue from "./components/ModalVue.vue";
import UserRepositories from "./components/UserRepositories.vue";
// composition API
import HomeComposition from "@/components/HomeComposition.vue";
// Cargando el componente de forma asincrona
import { defineAsyncComponent } from "vue";
const HelloWorld = defineAsyncComponent(() =>
  import("./components/HelloWorld.vue")
);

export default {
  name: "App",
  mixins: [base],
  components: {
    HelloWorld,
    MenuHeader,
    ModalVue,
    UserRepositories,
    HomeComposition,
  },
  data() {
    return {
      componente: "HelloWorld",
      show: false,
      text: "Hello Vue",
    };
  },
  beforeCreate() {
    console.log("beforeCreate", this.$data, this.$el);
  },
  created() {
    console.log("created", this.$data, this.$el);
  },
  mounted() {
    console.log("mounted", this.$data, this.$el);
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.fade-leave-active,
.fade-enter-active {
  transition: opacity 0.5s ease;
}
</style>
