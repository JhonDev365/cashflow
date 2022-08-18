<template>
  <div class="movements">
    <h2 class="title">Historial</h2>
    <div class="content">
      <Movement
        v-for="movement in movements"
        :key="movement.id"
        :title="movement.title"
      />
    </div>
  </div>
</template>
<!-- la variable movement recibe un props -->
<!-- vamos a utilizar Composition API -->
<!-- ya no necesitamos export default ni setup() -->
<script setup>
// defineProps: ejecuta una funcion que devuelve un objeto con los props
//xa poder usar los props dentro de la sintaxis de template necesitamos hacerlos
// reactivos con toRefs
import { toRefs, defineProps } from "vue";
import Movement from "./Movement.vue";

const props = defineProps({
  movements: {
    type: Array,
    // no podemos agregar un Array [] vacio, xq no tendriamos reactividad
    //necesitamos una funcion que nos devuelva una lista
    default: () => [],
  },
});

//destructuramos esta variable movements
const { movements } = toRefs(props);
</script>

<style scoped>
.movements {
  max-height: 100%;
  padding: 0 8px;
  margin-bottom: 14px;
}
.title {
  margin: 8px 16px 24px 16px;
  color: var(--brand-blue);
}
.content {
  max-height: 68vh;
  display: flex;
  flex-direction: column;
  gap: 8px;
  overflow-y: scroll;
}
</style>
