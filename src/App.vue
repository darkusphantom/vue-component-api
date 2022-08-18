<template>
  <p>Pokemon 1: {{text}}</p>
  <p>Pokemon 2: {{ text2 }} </p>
</template>

<script>
export default {
  name: 'App',
  components: {  },
  data: () => ({
    text: "Zangana",
    text2: "Dorime",
  }),
  methods: {
    async getPokemon() {
      const URL = 'https://pokeapi.co/api/v2/pokemon/255';
      const response = await fetch(URL);
      const data = await response.json();

      const URL2 = 'https://pokeapi.co/api/v2/pokemon/404';
      const response2 = await fetch(URL2);
      const data2 = await response2.json();

      this.text = data.name;
      this.text2 = data2.name;
    }
  },
  beforeCreate() {
    console.log("Before create", this.$data, this.$el);

  },
  created() {
    console.log("created", this.$data, this.$el);
    setTimeout(() => this.getPokemon(), 3000);
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
