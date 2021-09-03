<template>
  <v-container fluid class="px-2 pt-0 mt-5">
    <v-row justify="center" class="py-0">
      <v-col cols="12" md="4" class="py-0" v-for="(item, i) in month" :key="i">
        <v-card
          :color="colorFuncion(i)"
          class="headline font-weight-bold"
          max-width="90%"
          max-height="500"
        >
          <v-card-text>
            <v-row>
              <v-col cols="12" md="12" class="py-0">
                <center>
                  <b
                    ><h1 style="color: white">
                      {{ meses[item.month - 1] }}
                    </h1></b
                  >
                </center>
              </v-col>
              <v-progress-linear color="white"></v-progress-linear>
              <br />
              <v-col cols="6" md="6" class="py-0">
                <b style="color: white">Solicitud Comando/Senasir</b>
              </v-col>
              <v-col cols="6" md="6" class="py-0">
                <b style="color: white">Importaciones Comando/Senasir</b>
              </v-col>
              <v-col cols="6" md="6" class="py-0">
                <v-tooltip top>
                  <template v-slot:activator="{ on }">
                    <v-btn
                      fab
                      dark
                      small
                      :color="'info'"
                      bottom
                      right
                      v-on="on"
                      :loading="loading_sc && i == index"
                      @click="
                        index = i;
                        solicitudComando();
                      "
                    >
                      <v-icon style="color: white"
                        >mdi-city-variant-outline</v-icon
                      >
                    </v-btn>
                  </template>
                  <div>
                    <span>Solicitud Comando</span>
                  </div>
                </v-tooltip>
                <v-tooltip top>
                  <template v-slot:activator="{ on }">
                    <v-btn
                      fab
                      dark
                      small
                      :color="'info'"
                      right
                      v-on="on"
                      :loading="loading_ss && i == index"
                      @click.stop="
                        index = i;
                        solicitudSenasir('S', item.id);
                      "
                    >
                      <v-icon style="color: white">mdi-city</v-icon>
                    </v-btn>
                  </template>
                  <div>
                    <span>Solicitud Senasir</span>
                  </div>
                </v-tooltip>
              </v-col>
              <v-col cols="6" md="6" class="py-0">
                <v-tooltip top>
                  <template v-slot:activator="{ on }">
                    <v-btn
                      fab
                      dark
                      small
                      :color="'info'"
                      bottom
                      right
                      v-on="on"
                      @click.stop="importacionComando(item.month, item.id)"
                    >
                      <v-icon style="color: white">mdi-warehouse</v-icon>
                    </v-btn>
                  </template>
                  <div>
                    <span>Importación Comando</span>
                  </div>
                </v-tooltip>
                <v-tooltip top>
                  <template v-slot:activator="{ on }">
                    <v-btn
                      fab
                      dark
                      small
                      :color="'info'"
                      right
                      v-on="on"
                      @click.stop="importacionSenasir(item.month, item.id)"
                    >
                      <v-icon style="color: white">mdi-home-analytics</v-icon>
                    </v-btn>
                  </template>
                  <div>
                    <span>Importación Senasir</span>
                  </div>
                </v-tooltip>
              </v-col>
            </v-row>
          </v-card-text>
          <v-progress-linear color="white"></v-progress-linear>
          <v-card-actions>
            <v-col cols="4" md="8" class="py-0">
              <b style="color: white" class="caption"
                >Reportes Comando/Senasir</b
              >
            </v-col>
            <v-tooltip top>
              <template v-slot:activator="{ on }">
                <v-btn
                  fab
                  dark
                  small
                  :color="'#454545'"
                  bottom
                  right
                  v-on="on"
                  @click.stop="reporteComandoSenasir(item.id, 'C', i)"
                >
                  <v-icon>mdi-warehouse</v-icon>
                </v-btn>
              </template>
              <div>
                <span>Reporte Pago Comando</span>
              </div>
            </v-tooltip>
            <v-tooltip top>
              <template v-slot:activator="{ on }">
                <v-btn
                  fab
                  dark
                  small
                  :color="'#454545'"
                  bottom
                  right
                  v-on="on"
                  @click.stop="reporteComandoSenasir()"
                >
                  <v-icon>mdi-home-analytics</v-icon>
                </v-btn>
              </template>
              <div>
                <span>Reporte Pago Senasir</span>
              </div>
            </v-tooltip>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "ImportExport",
  data() {
    return {
      //data para los loadings
      index: -1,
      loading_sc: false,
      loading_ss: false,
      //colores
      color1: "#454545",
      color2: "#000",
      //
      titulo: "Hola simportaciones",
      month: [],
      meses: [
        "ENERO",
        "FEBRERO",
        "MARZO",
        "ABRIL",
        "MAYO",
        "JUNIO",
        "JULIO",
        "AGOSTO",
        "SEPTIEMBRE",
        "OCTUBRE",
        "NOVIEMBRE",
        "DICIEMBRE",
      ],
    };
  },
  beforeMount() {
    this.month = [
      { month: 7, import_senasir: true, import_comando: true },
      { month: 8, import_senasir: true, import_comando: true },
      { month: 9, import_senasir: true, import_comando: false },
    ];
  },
  methods: {
    async solicitudComando() {
      this.loading_sc = true;
      console.log(this.index);
      await new Promise((resolve) => setTimeout(resolve, 1000));

      this.loading_sc = false;
      this.index = -1;
    },
    async solicitudSenasir() {
      this.loading_ss = true;
      console.log(this.index);
      await new Promise((resolve) => setTimeout(resolve, 1000));

      this.loading_ss = false;
      this.index = -1;
    },
    colorFuncion(i) {
      console.log(this.month[i].import_senasir);
      if (this.month[i].import_senasir && this.month[i].import_comando)
        return "#454545";
      else return "pink";
    },
  },
  computed: {},
};
</script>

<style>
</style>