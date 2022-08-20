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
        :totalAmount="totalAmount"
        :amount="amount"
      >
        <template #graphic>
          <!-- yapodemos pasarle y recibir las props amounts a graphic -->
          <Graphic :amounts="amounts" @select="select" />
        </template>
        <template #action>
          <Action @create="create" />
        </template>
      </Resume>
    </template>
    <template #movements>
      <Movements :movements="movements" @remove="remove" />
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
        // {
        //   id: 0,
        //   title: "Ruta Cal51",
        //   description: "Supercercado Comfandi",
        //   amount: 500,
        //   time: new Date("08-08-2022"),
        // },
        // {
        //   id: 1,
        //   title: "Ruta Cal52",
        //   description: "C.C. La Estación",
        //   amount: 200,
        //   time: new Date("08-09-2022"),
        // },
        // {
        //   id: 2,
        //   title: "Ruta Cal52",
        //   description: "Ramsa",
        //   amount: -300,
        //   time: new Date("08-10-2022"),
        // },
        // {
        //   id: 3,
        //   title: "Ruta Cal53",
        //   description: "Nutresa",
        //   amount: 250,
        //   time: new Date("08-11-2022"),
        // },
        // {
        //   id: 4,
        //   title: "Ruta Cal54",
        //   description: "Popsy",
        //   amount: -100,
        //   time: new Date("08-12-2022"),
        // },
        // {
        //   id: 5,
        //   title: "Ruta Cal54",
        //   description: "Popsy",
        //   amount: 0,
        //   time: new Date("08-13-2022"),
        // },
        // {
        //   id: 6,
        //   title: "Ruta Cal54",
        //   description: "Popsy",
        //   amount: 300,
        //   time: new Date("08-14-2022"),
        // },
        // {
        //   id: 7,
        //   title: "Ruta Cal54",
        //   description: "Popsy",
        //   amount: 100,
        //   time: new Date("08-15-2022"),
        // },
        // {
        //   id: 8,
        //   title: "Ruta Cal54",
        //   description: "Popsy",
        //   amount: 480,
        //   time: new Date("07-09-2022"),
        // },
        // {
        //   id: 9,
        //   title: "Ruta Cal54",
        //   description: "Popsy",
        //   amount: -350,
        //   time: new Date("07-10-2022"),
        // },
      ],
    };
  },
  computed: {
    amounts() {
      const lastDays = this.movements
        .filter((m) => {
          const today = new Date();
          const oldDate = today.setDate(today.getDate() - 30);
          return m.time >= oldDate;
        })
        .map((m) => m.amount);

      return lastDays.map((m, i) => {
        const lastMovements = lastDays.slice(0, i + 1);
        return lastMovements.reduce((suma, movement) => {
          return suma + movement;
        }, 0);
      });
    },
    totalAmount() {
      return this.movements.reduce((suma, m) => {
        return suma + m.amount;
      }, 0);
    },
  },
  // de incicio nos dara una lsita vacia, para recuperar los elementos,nos basamos en
  //ciclo de vida de vue,con mounted, cuano Home.vue ya se monto entoces recuperar es valor
  //y mandarlo a la lista de movements
  mounted() {
    const movements = JSON.parse(localStorage.getItem("movements"));
    //obligar a que las fechas este en su foramto de fecha
    //vamos a crear validacion para asegurar que recibimos un array
    //con esta vlidacion de js Array.isArray(nombrearray)
    if (Array.isArray(movements)) {
      this.movements = movements?.map((m) => {
        return { ...m, time: new Date(m.time) };
      });
    }
  },
  methods: {
    //recibe como argumento, el movimiento que acabamos de enviar
    create(movement) {
      this.movements.push(movement);
      this.save();
    },
    remove(id) {
      const index = this.movements.findIndex((m) => m.id === id);
      console.log(index);
      this.movements.splice(index, 1);
      this.save();
    },
    save() {
      //almacenar en local, setItem('nombrede mis datos en local',.this.la vaiable donde lo gurdarmeos)
      //de forma mas segura convertirlo en cadena de texto
      localStorage.setItem("movements", JSON.stringify(this.movements));
    },
    select(el) {
      console.log(el);
      this.amount = el;
    },
    //otra alternativa pero nofunciona
    // remove(id) {
    //   this.movements = this.movements.filter((m) => m.id != id);
    // },
  },
};
</script>
