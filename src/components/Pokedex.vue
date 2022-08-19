<template>
  <div class="container">
    <div class="pokemon">
      <p class="pokemon-name">
        Pokemon 1:
        <span>
          {{ pokemon1.name }}
        </span>
      </p>
      <img :src="pokemon1.image" :alt="pokemon1.name">
    </div>
    <div class="pokemon">
      <p class="pokemon-name">
        Pokemon 2:
        <span>
          {{ pokemon2.name }}
        </span>
      </p>
      <img :src="pokemon2.image" :alt="pokemon2.name">
    </div>
  </div>
  <p>Texto: {{ text }}</p>
  <button type="button" ref="btn">Reset</button>
</template>
<script setup>
import { defineProps, ref, toRefs, watch, computed } from 'vue';

const props = defineProps({
  pokemon1: {
    type: Object,
    default: () => {},
  },
  pokemon2: {
    type: Object,
    default: () => {},
  },
});

const { pokemon1, pokemon2 } = toRefs(props);

const firstname = ref("Dorime");
const lastname = ref("Ameno");

const text = computed(()=> (`${firstname.value}  ${lastname.value}`));

const btn = ref(null);
watch(btn, (valor) => {
  console.log(valor);
});

</script>

<styles lang="scss">
.container {
  display: flex;

  .pokemon {
    margin: 0 10px;
  }

  .pokemon-name {
    display: flex;
    flex-direction: column;
    text-transform: capitalize;

    span {
      margin-top: 6px;
    }
  }
}
</styles>
