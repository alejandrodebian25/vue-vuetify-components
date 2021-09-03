<template>
  <v-content>
    <h1>Boletas de pago {{ test }}</h1>
    <v-row>
      <v-col cols="10">
        <v-data-table
          :headers="_headers"
          :items="pagos"
          :items-per-page="5"
          class="elevation-1"
          hide-default-footer
        >
        </v-data-table>
      </v-col>
    </v-row>
  </v-content>
</template>

<script>
export default {
  name: "Boletas",
  data: () => ({
    test: "verdad",
    tipo: "comision",
    headers: [
      {
        text: "Periodo",
        align: "start",
        sortable: false,
        value: "periodo",
        show: ["activo", "pasivo", "comision"],
      },
      {
        text: "Liquido",
        value: "liquido",
        show: ["activo", "pasivo", "comision"],
      },
      {
        text: "Monto de ajuste",
        value: "monto_de_ajuste",
        show: ["activo", "pasivo", "comision"],
      },
      {
        text: "Bono Frontera",
        value: "bono_frontera",
        show: ["activo", "pasivo", "comision"],
      },
      { text: "Bono Cargo", value: "bono_cargo", show: ["activo"] },
      { text: "Bono Oriente", value: "bono_oriente", show: ["activo"] },
      { text: "Bono Seguridad", value: "bono_seguridad", show: ["activo"] },
      { text: "Bono Renta", value: "bono_renta", show: ["pasivo"] },
    ],
    pagos: [
      {
        periodo: "01/01/01",
        liquido: "4532.80",
        monto_de_ajuste: 1.0,
        bono_frontera: 2.0,
        bono_cargo: 3.0,
        bono_oriente: 4.0,
        bono_seguridad: 5.0,
        bono_renta: 6.0,
      },
    ],
  }),
  computed: {
    _headers() {
      if (this.tipo == "pasivo") {
        return this.headers.filter((x) => x.show.includes("pasivo"));
      }
      if (this.tipo == "activo") {
        return this.headers.filter((x) => x.show.includes("activo"));
      }
      if (this.tipo == "comision") {
        return this.headers.filter((x) => x.show.includes("comision"));
      }
      return this.headers;
      //   return this.headers.filter((x) => x.show);
    },
  },
};
</script>

<style>
</style>