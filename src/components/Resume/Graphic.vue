<template>
  <div>
    <svg viewBox="0,0 300 200">
      <line
        stroke="#c4c4c4"
        stroke-width="2"
        x1="0"
        y1="100"
        x2="300"
        y2="100"
      />
      <!-- en polyline (0,0)  es esq-sup-izq, (max,max) esq-inf-der -->
      <!-- cremos una una funcion computada que trasforme
      los montos en coord de px con los puntos -->
      <polyline
        fill="none"
        stroke="#0689b0"
        stroke-width="2"
        :points="points"
      />
      <line
        stroke="#04b500"
        stroke-width="2"
        x1="200"
        y1="0"
        x2="200"
        y2="200"
      />
    </svg>
    <p>Ultimos 30 días</p>
  </div>
</template>

<script setup>
import { defineProps, toRefs, computed } from "vue";
const props = defineProps({
  //para que sa reactiva debe ser una funcion
  amounts: {
    type: Array,
    default: () => [],
  },
});

//para que sea reactivo usamos torefs
//destrucutramos lavariable
const { amounts } = toRefs(props);
const amountToPixels = () => {
  const min = Math.min(...amounts.value);
  const max = Math.max(...amounts.value);
  return `${min}, ${max}`;
};
//para convertir amounts que viene de Home en points debemos dividir la
//grafica entre los montos, para el eje y ddebemos convertirlo para que
//quepa dentro del esacio en pixeles de la grafica
const points = computed(() => {
  const total = amounts.value.length;

  return Array(total)
    .fill(100)
    .reduce((points, amount, i) => {
      const x = (300 / total) * (i + 1);
      const y = amountToPixels(amount);
      return `${points} ${x},${y}`;
    }, "0, 100");
});
</script>

<style scoped>
svg {
  width: 100%;
}

p {
  text-align: center;
}
</style>
