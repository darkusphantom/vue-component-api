<template>
  <Pokedex
    :pokemon1="pokemon1"
    :pokemon2="pokemon2"
  />
</template>

<!--script setup-->
<!-- Si vas a utilizar el export default, asegurate de no tener el atributo setup en el script.
  De lo contrario tendra conflictos en saber cual elemento se está exportando-->
<script>
import Pokedex from './components/Pokedex.vue';

/*
import { defineProps, defineExpose, ref, toRefs, computed, watch, inject } from 'vue';
const props = defineProps({ //Devuelva la variable props
  pokemon1: String,
  pokemon2: String,
})

const { pokemon1, pokemon2 } = toRefs(props);

const pokemons = computed(() => {
  return `${text1} y ${text2}`;
});

const pokes = inject("pokes");

defineExpose({
  pokes
})

const btn = ref(null);
console.log(btn.value);

watch(btn, (valor) => {
  console.log(valor);
});
*/


export default {
  name: 'App',
  components: {
    Pokedex,
  },
  //setup(props, {expose}) {}
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
      console.log(pokemon);

      dataPokemon.name === 'torchic'
        ? this.pokemon1 = dataPokemon
        : this.pokemon2 = dataPokemon;
    }
  },
  beforeCreate() {
    //console.log("Before create", this.$data, this.$el);

  },
  created() {
    //console.log("created", this.$data, this.$el);
    setTimeout(() => {
      this.getPokemon(255);
      this.getPokemon(404);
    }, 3000)
  },
  mounted() {
    //console.log("Mounted", this.$data, this.$el);
  }
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
