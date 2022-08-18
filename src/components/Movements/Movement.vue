<template>
  <div class="movement">
    <div class="content">
      <h4>{{ title }}</h4>
      <p>{{ description }}</p>
    </div>
    <div class="action">
      <img src="@/assets/trash-icon.svg" alt="delete" @click="remove" />
      <p :class="{ red: isNegative, green: !isNegative }">
        {{ amountCurrency }}
      </p>
    </div>
  </div>
</template>

<!-- para definir prop usamos define propsdentro de una sintaxis // Composition Api -->

<script setup>
//para progpagar el evento haci afuera usamos defineEmit
import { toRefs, defineProps, defineEmits, computed } from "vue";
const currencyFormater = new Intl.NumberFormat("es-CO", {
  style: "currency",
  currency: "COP",
});

const props = defineProps({
  id: {
    type: Number,
  },
  title: {
    type: String,
  },
  description: {
    type: String,
  },
  amount: {
    type: Number,
  },
});

//usamos destructuracion, torefs para usarlo en el template
const { id, title, description, amount } = toRefs(props);

//funcion computada
const amountCurrency = computed(() => currencyFormater.format(amount.value));

//funcion apra agregar la clase red si el valor es negativo
const isNegative = computed(() => amount.value < 0);

// enviamos el evento remove a quien lo usa, el compoennte padre
const emit = defineEmits(["remove"]);

//agregamos la funcion de elimianr movimiento
const remove = () => {
  emit("remove", id.value);
};
</script>

<style scoped>
.movement {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 16px;
  background-color: #e6f9ff;
  border-radius: 8px;
  box-sizing: border-box;
}
.movement .content {
  width: 100%;
}
.movement .action {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  flex-direction: column;
}
h4,
p {
  margin: 0;
  padding: 0;
}
h4 {
  margin-bottom: 8px;
}
.movement .action img {
  margin-bottom: 16px;
}
.red {
  color: red;
}
.green {
  color: green;
}
</style>
