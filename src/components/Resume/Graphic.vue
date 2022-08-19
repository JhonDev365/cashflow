<template>
  <div>
    <!--para escuchar cuando tocamos la pantalla necesitamos 3 eventos -->
    <svg
      @touchstart="tap"
      @touchmove="tap"
      @touchend="untap"
      viewBox="0,0 300 200"
    >
      <line
        stroke="#c4c4c4"
        stroke-width="2"
        x1="0"
        :y1="zero"
        x2="300"
        :y2="zero"
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
        v-show="showPointer"
        stroke="#04b500"
        stroke-width="2"
        :x1="pointer"
        y1="0"
        :x2="pointer"
        y2="200"
      />
    </svg>
    <p>Ultimos 30 días</p>
    <div>{{ zero }}</div>
  </div>
</template>

<script setup>
import { defineProps, toRefs, ref, computed } from "vue";
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

const amountToPixels = (amount) => {
  const min = Math.min(...amounts.value);
  const max = Math.max(...amounts.value);

  const amountAbs = amount + Math.abs(min);
  const minmax = Math.abs(max) + Math.abs(min);

  return 200 - ((amountAbs * 100) / minmax) * 2;
};

const zero = computed(() => {
  return amountToPixels(0);
});

//para convertir amounts que viene de Home en points debemos dividir la
//grafica entre los montos, para el eje y ddebemos convertirlo para que
//quepa dentro del esacio en pixeles de la grafica
const points = computed(() => {
  const total = amounts.value.length;

  return amounts.value.reduce((points, amount, i) => {
    const x = (300 / total) * (i + 1);
    const y = amountToPixels(amount);
    return `${points} ${x},${y}`;
  }, "0, 100");
});

const showPointer = ref(false);
const pointer = ref(0);
//creamos las funciones para tap y untap de los eventos touch
const tap = ({ target, touches }) => {
  showPointer.value = true;
  //elementWidth. tamaño de SVG
  const elementWidth = target.getBoundingClientRect().width;
  //elelemntX, donde comienza en el eje X, osea la izquierda del SVG
  const elementX = target.getBoundingClientRect().x;
  //touchX la barra que se genera al tocar el display en cooord x
  const touchX = touches[0].clientX;
  pointer.value = ((touchX - elementX) * 300) / elementWidth;
};
//para ocultar creamos untap, sin argumento ya que no ocupamos el evento perset, solo deseamos escuchar cuadno sucede
const untap = () => {
  showPointer.value = false;
};
</script>

<style scoped>
svg {
  width: 100%;
}

p {
  text-align: center;
}
</style>
