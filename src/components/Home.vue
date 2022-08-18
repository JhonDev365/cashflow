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
      />
    </template>
    <template #movements>
      <Movements />
    </template>
  </Layout>
</template>

<script>
import Layout from "./Layout.vue";
import Header from "./Header.vue";
import Resume from "./Resume/Index.vue";
import Movements from "./Movements.vue";

export default {
  components: {
    Layout,
    Header,
    Resume,
    Movements,
  },
  data() {
    return {
      label: null,
      amount: null,
    };
  },
};
</script>
