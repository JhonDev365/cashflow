<template>
  <div class="movements">
    <!-- <h2 class="title">Historial</h2> -->
    <h2 class="title">Placa: VCS249</h2>
    <h3 class="title">Conductor: Wilmar Ibañez</h3>
    <div class="content">
      <!-- <Movement
        v-for="movement in movements"
        :key="movement.id"
        :title="movement.title"
        :description="movement.description"
        :amount="movement.amount"
      /> -->
      <!--otra forma de hacerlo seria -->
      <Movement
        v-for="{ id, title, description, amount } in movements"
        :key="id"
        :title="title"
        :description="description"
        :amount="amount"
        @remove="remove"
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

//ahcemos una funcion handler para escuchar la props remove
const remove = (id) => {
  console.log("remove", id);
};
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
