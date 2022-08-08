<template>
  <p>{text}</p>
</template>

<script>

export default {
  name: 'App',
  components: {  },
  data() {
    return {
      text: "Zangana"
    }
  },
  beforeCreate() {
    console.log("Before create", this.$data, this.$el);
  },
  created() {
    console.log("created", this.$data, this.$el);
  },
  mounted() {
    console.log("Mounted", this.$data, this.$el);
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
