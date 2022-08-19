<template>
  <Layout>
    <template #header>
      <Header />
    </template>
    <template #resume>
      <!-- :totalLabel="'Ahorro total'" -->
      <Resume
        :totalLabel="'Historial de ruta'"
        :label="label"
        :totalAmount="30000"
        :amount="amount"
      >
        <template #graphic>
          <!-- yapodemos pasarle y recibir las props amounts a graphic -->
          <Graphic :amounts="amounts" />
        </template>
        <template #action>
          <Action />
        </template>
      </Resume>
    </template>
    <template #movements>
      <Movements :movements="movements" />
    </template>
  </Layout>
</template>

<script>
import Layout from "./Layout.vue";
import Header from "./Header.vue";
import Resume from "./Resume/Index.vue";
import Movements from "./Movements/Index.vue";
import Action from "./Action.vue";
import Graphic from "./Resume/Graphic.vue";

export default {
  components: {
    Layout,
    Header,
    Resume,
    Movements,
    Action,
    Graphic,
  },
  //En la función data, se agrega la variable 'label'
  // y se envía como parametro de 'label' en el template `Resume`
  data() {
    return {
      label: null,
      amount: null,
      movements: [
        {
          id: 0,
          title: "Ruta Cal51",
          description: "Supercercado Comfandi",
          amount: 500,
        },
        {
          id: 1,
          title: "Ruta Cal52",
          description: "C.C. La Estación",
          amount: 200,
        },
        {
          id: 2,
          title: "Ruta Cal52",
          description: "Ramsa",
          amount: -300,
        },
        {
          id: 3,
          title: "Ruta Cal53",
          description: "Nutresa",
          amount: 250,
        },
        {
          id: 4,
          title: "Ruta Cal54",
          description: "Popsy",
          amount: -100,
        },
        {
          id: 5,
          title: "Ruta Cal54",
          description: "Popsy",
          amount: 0,
        },
        {
          id: 6,
          title: "Ruta Cal54",
          description: "Popsy",
          amount: 300,
        },
        {
          id: 7,
          title: "Ruta Cal54",
          description: "Popsy",
          amount: 100,
        },
        {
          id: 8,
          title: "Ruta Cal54",
          description: "Popsy",
          amount: 480,
        },
        {
          id: 9,
          title: "Ruta Cal54",
          description: "Popsy",
          amount: -350,
        },
      ],
    };
  },
};
</script>
