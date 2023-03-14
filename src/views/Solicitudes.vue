<template>
  <div
    class="container d-flex justify-center align-center"
    style="height: 80vh"
  >
    <v-row>
      <v-col cols="12" md="6">
        <v-card
          style="cursor: pointer"
          class="card-solicitudes d-flex justify-center align-center"
          height="100px"
          width="100%"
          @click="openSolic('Reparacion')"
        >
          <div>
            <h4>SOLICITUD DE REPARACIÓN DE EQUIPOS</h4>
          </div>
        </v-card>
      </v-col>
      <v-col cols="12" md="6">
        <v-card
          style="cursor: pointer"
          class="card-solicitudes d-flex justify-center align-center"
          height="100px"
          width="100%"
          @click="openSolic('Habilitacion')"
        >
          <div>
            <h4>SOLICITUD DE ASIGNACIÓN DE ROLES</h4>
          </div>
        </v-card>
      </v-col>
    </v-row>
    <v-dialog
      v-model="openSolicitud"
      transition="dialog-top-transition"
      max-width="600"
    >
      <componente :is="solicitud"></componente>
    </v-dialog>
  </div>
</template>
<script>
import Reparacion from "@/components/Solicitudes/Reparacion";
import Habilitacion from "@/components/Solicitudes/Habilitacion";
export default {
  components: { Reparacion, Habilitacion },
  data() {
    return {
      openSolicitud: false,
      solicitud: "",
    };
  },
  methods: {
    openSolic(name) {
      this.openSolicitud = true;
      this.solicitud = name;
    },
  },
};
</script>
<style>
.card-solicitudes:hover {
  background: #00acc1;
  color: #fff;
}
</style>
