<template>
  <div class="modal">
    <div class="head">
      <!-- <p>Nuevo movimiento</p> -->
      <p>Nueva Ruta</p>
      <img @click="close" src="@/assets/close-icon.svg" alt="cerrar" />
    </div>
    <div class="body">
      <slot></slot>
    </div>
  </div>
</template>

<script setup>
//para q funcione la funcion cerrar, debemos crear un emit
import { defineEmits } from "vue";

//nombrarlo ocmo lo necesite, evitando homonimia
const emit = defineEmits(["close"]);
// crear funcion que permite cerrar el modal
const close = () => emit("close");
</script>

<style scoped>
.modal {
  z-index: 2;
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  background-color: white;
}

.head {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 24px 24px;
  box-sizing: border-box;
}

p {
  margin: 0;
  font-size: 1.5rem;
  color: var(--brand-blue);
}
</style>
