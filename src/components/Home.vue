<template>
  <Layout>
    <template #header>
      <Header />
    </template>
    <template #resume>
      <Resume
        :totalLabel="'Ahorro total'"
        :label="label"
        :totalAmount="30000"
        :amount="amount"
      >
        <template #graphic>
          <!-- yapodemos traer el props amounts desde graphic -->
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
      amounts: [500, 200, -300, 250, -100, 0, 300],
      movements: [
        {
          id: 0,
          title: "Movimiento 1",
          description: "Pago de servicios públicos",
          amount: 1000,
        },
        {
          id: 1,
          title: "Movimiento 2",
          description: "Pago de servicios públicos",
          amount: 1000,
        },
        {
          id: 2,
          title: "Movimiento 3",
          description: "Pago de servicios públicos",
          amount: -3500,
        },
        {
          id: 3,
          title: "Movimiento 4",
          description: "Pago de servicios públicos",
          amount: 2000,
        },
        {
          id: 4,
          title: "Movimiento 5",
          description: "Pago de servicios públicos",
          amount: -2000,
        },
      ],
    };
  },
};
</script>
