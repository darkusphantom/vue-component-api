<template>
  <button @click="show = !show">Menu</button>
  <transition name="fade">
    <Menu v-show="show"/>
  </transition>
</template>

<script>
import Menu from './components/Menu.vue';

export default {
  name: 'App',
  components: {
    Menu
  },
  data() {
    return {
      show: false,
    };
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.fade-leave-to {
  opacity: 0;
}

//Nombre de la transicion, el momento en que se ejecuta y el tiempo
.fade-leave-active,
.fade-enter-active {
  transition: opacity 0.5s ease;
}
</style>
