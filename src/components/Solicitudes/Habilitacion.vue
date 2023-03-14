<template>
  <v-card>
    <v-card-text>
      <div class="pt-5">
        <v-row>
          <h4>DATOS AMBIENTE</h4>
          <v-col cols="12">
            <v-select
              outlined
              dense
              label="Ambiente"
              :items="['HML', 'PRODUCCIÓN']"
            ></v-select>
          </v-col>
        </v-row>
        <v-row v-for="persona in personas" :key="persona">
          <v-row class="d-flex justify-space-between align-center">
            <h4>DATOS PERSONA</h4>
            <div class="d-flex">
              <v-btn v-if="persona > 1" icon @click="personas -= 1">
                <v-icon color="grey lighten-1">mdi-close</v-icon>
              </v-btn>
              <v-btn icon @click="personas += 1">
                <v-icon color="grey lighten-1">mdi-plus</v-icon>
              </v-btn>
            </div>
          </v-row>
          <v-col cols="12">
            <v-text-field dense outlined label="Cuit/Cuil"></v-text-field>
          </v-col>
          <v-col cols="12" class="mt-n10">
            <v-select dense outlined label="Roles"></v-select>
          </v-col>
          <v-col cols="12" class="mt-n10">
            <v-text-field dense outlined label="Email"></v-text-field>
          </v-col>
          <v-col cols="12" class="mt-n10">
            <v-text-field dense outlined label="Teléfono"></v-text-field>
          </v-col>
        </v-row>
      </div>
    </v-card-text>
    <v-card-actions class="justify-end"></v-card-actions>
  </v-card>
</template>
<script>
export default {
  data() {
    return {
      personas: 1,
    };
  },
};
</script>
