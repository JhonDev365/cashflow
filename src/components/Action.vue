<template>
  <!-- <button @click="showModal = true">Agregar movimiento</button> -->
  <button @click="showModal = true">Agregar Ruta</button>
  <!-- utilizamos teleport para enviar el modal a otra parte del DOM 
  podemos declarar el codigo del componente y poder tener en un mismo archivo .vue
  los 2 componentes y tener organizado nuestro proyecto  -->
  <teleport to="#app">
    <!-- para que funcione la varible v-show se debe importar Ref
    y crear la variable -->
    <Modal v-show="showModal" @close="showModal = false">
      <!-- como utilizamos un slot default, no es necsario el tag tempalte -->
      <form @submit.prevent="submit">
        <div class="field">
          <!-- <label>Título</label> -->
          <label>Ruta</label>
          <input type="text" v-model="title" />
        </div>
        <div class="field">
          <label>Conductor</label>
          <textarea rows="4" v-model="description"></textarea>
        </div>
        <div class="field">
          <label>Descripción</label>
          <textarea rows="4" v-model="description"></textarea>
        </div>
        <div class="field">
          <!-- <label>Monto</label> -->
          <label>Monto facturas</label>
          <input type="number" v-model="amount" />
        </div>
        <div class="field">
          <!-- radio button nos permiten seleccionar opciones multipkles -->
          <label class="radio-label">
            <input type="radio" v-model="movementType" value="Ingreso" />
            <!-- <span>Ingreso</span> -->
            <span>Visita Efectiva</span>
          </label>
          <label class="radio-label">
            <input type="radio" v-model="movementType" value="Gasto" />
            <!-- <span>Gasto</span> -->
            <span>Visita No Efectiva</span>
          </label>
        </div>
        <div class="action">
          <!-- no se agrega evento click xq de forma nativa button tieen submit
            solo debemos escucharlo en el form -->
          <!-- <button>Agregar movimiento</button> -->
          <button>Agregar Ruta</button>
        </div>
      </form>
    </Modal>
  </teleport>
</template>

<script setup>
import { ref } from "vue";
import Modal from "./Modal.vue";

const showModal = ref(false);
const title = ref("");
const amount = ref(0);
const description = ref("");
const movementType = ref("Ingreso");

//creamos funcion submit para enviar y cerrar formulario
const submit = () => {
  // showModal.value = false;
  //o tambien:
  showModal.value = !showModal.value;
};
</script>

<style scoped>
button {
  color: white;
  font-size: 1.25rem;
  background-color: var(--brand-blue);
  border: none;
  width: 100%;
  padding: 24px 60px;
  border-radius: 60px;
  box-sizing: border-box;
}

form {
  font-size: 1.24rem;
  width: 100%;
}

form .action {
  padding: 0 24px;
}

.field {
  display: flex;
  justify-content: space-between;
  flex-direction: column;
  padding: 16px 24px;
}

label {
  margin-bottom: 8px;
}

input,
textarea {
  font-size: 1.24rem;
  border: 2px solid var(--brand-blue);
  border-radius: 8px;
  padding: 8px;
}

input[type="number"] {
  text-align: right;
}

.radio-label {
  display: flex;
  align-items: center;
  margin-top: 8px;
}

.radio-label span {
  margin-top: 4px;
  margin-left: 8px;
}

input[type="radio"] {
  appearance: none;
  width: 1.24rem;
  height: 1.24rem;
  color: var(--brand-blue);
  border: 2px solid var(--brand-blue);
  border-radius: 50%;
}

input[type="radio"]:checked {
  background-color: var(--brand-blue);
}
</style>
