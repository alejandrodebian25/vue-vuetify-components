<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />

        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png"
          width="100"
        />
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
        text
      >
        <span class="mr-2">Latest Release</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <Boletas :pagos="pagos"/>
      <!-- <Boletas /> -->
    </v-main>
  </v-app>
</template>

<script>
import Boletas from "./components/BoletasAjuste";

export default {
  name: "App",

  components: {
    Boletas,
  },

  data: () => ({
    mensaje: {},
    //Datos para componenete Bolretas AJUSte
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
};
</script>
