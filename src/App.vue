<template>
  <Pokedex
    :pokemon1="pokemon1"
    :pokemon2="pokemon2"
  />
  <p>Texto: {{ text }}</p>
  <p>Counter: {{ obj }}</p>
</template>

<script>
import { ref, reactive, watch } from 'vue';
import Pokedex from './components/Pokedex.vue';

export default {
  name: 'App',
  components: {
    Pokedex,
  },
  data: () => ({
    pokemon1: {},
    pokemon2: {},
  }),
  methods: {
    async getPokemon(id) {
      try {
        const URL = `https://pokeapi.co/api/v2/pokemon/${id}`;
        const response = await fetch(URL);
        const pokemon = await response.json();
        this.setPokemon(pokemon);
      } catch( error ) {
        console.error(error);
      }
    },
    setPokemon(pokemon) {
      const dataPokemon = {
        name: pokemon.name,
        image: pokemon.sprites.front_default,
      };

      dataPokemon.name === 'torchic'
        ? this.pokemon1 = dataPokemon
        : this.pokemon2 = dataPokemon;
    }
  },
  created() {
    setTimeout(() => {
      this.getPokemon(255);
      this.getPokemon(404);
    }, 3000)
  },
  setup() {
    const text = ref('Hola vue');
    const obj = reactive({
      counter: 0,
    });

    setInterval(() => obj.counter++, 500);
    console.log(obj.counter);

    watch(obj, (value, prev) => {
      console.log(value, prev);
    });

    return {
      text,
      obj
    };
  },
}
</script>

<style lang="scss">
body {
  display: grid;
  place-items: center;
}
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
