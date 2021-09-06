<template>
  <v-data-table
    :headers="_headers"
    :items="pagos"
    item-key="id"
    hide-default-footer
  >
    <!-- <template v-slot:item="{ item }">
      <tr>
        <td>{{ item.periodo }}</td>
        <td>{{ item.liquido }}</td>
        <td>{{ item.monto_de_ajuste }}</td>
        <td>{{ item.bono_frontera }}</td>
        <td>{{ item.bono_cargo }}</td>
        <td>{{ item.bono_oriente }}</td>
        <td>{{ item.bono_seguridad }}</td>
        <td>{{ item.bono_renta }}</td>
      </tr>
    </template> -->
    <template slot="body.append">
      <tr class="dark--text">
        <td>Totals</td>
        <td>121212</td>
        <td>812121</td>
        <td v-show="tipo == 'activo'">712121</td>
        <td v-show="tipo == 'activo'">612121</td>
        <td v-show="tipo == 'activo'">512121</td>
        <td v-show="tipo == 'activo'">412121</td>
        <td v-show="tipo == 'pasivo'">312121</td>
      </tr>
    </template>
  </v-data-table>
</template>

<script>
export default {
  name: "BoletasAjuste",
  props: {
    pagos: {
      type: Array,
      required: true,
    },
  },
  data: () => ({
    tipo: "comision",
    headers: [
      {
        text: "Periodo",
        align: "start",
        sortable: false,
        value: "periodo",
        show: ["all"],
      },
      {
        sortable: false,
        text: "Liquido",
        value: "liquido",
        show: ["all"],
      },
      {
        text: "Monto de ajuste",
        value: "monto_de_ajuste",
        show: ["all"],
      },
      {
        text: "Bono Frontera",
        value: "bono_frontera",
        show: ["activo"],
      },
      { text: "Bono Cargo", value: "bono_cargo", show: ["activo"] },
      { text: "Bono Oriente", value: "bono_oriente", show: ["activo"] },
      { text: "Bono Seguridad", value: "bono_seguridad", show: ["activo"] },
      { text: "Bono Renta", value: "bono_renta", show: ["pasivo"] },
    ],
  }),
  computed: {
    _headers() {
      if (this.tipo == "pasivo") {
        return this.headers.filter(
          (x) => x.show.includes("pasivo") || x.show.includes("all")
        );
      }
      if (this.tipo == "activo") {
        return this.headers.filter(
          (x) => x.show.includes("activo") || x.show.includes("all")
        );
      }
      if (this.tipo == "comision") {
        return this.headers.filter(
          (x) => x.show.includes("comision") || x.show.includes("all")
        );
      }
      return this.headers;
      //   return this.headers.filter((x) => x.show);
    },
  },
};
</script>

<style>
</style>