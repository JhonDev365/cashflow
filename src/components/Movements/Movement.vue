<template>
  <div class="movement">
    {{ title }}
  </div>
</template>

<!-- para definir prop usamos define propsdentro de una sintaxis // Composition Api -->

<script setup>
import { toRefs, defineProps } from "vue";
const props = defineProps({
  title: {
    type: String,
  },
});

//usamos destructuracion, torefs para usarlo en el template
const { title } = toRefs(props);
</script>
