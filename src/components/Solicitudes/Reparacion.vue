<template>
  <v-card>
    <v-card-text>
      <div class="pt-5">
        <v-row>
          <h4>DATOS SOLICITUD</h4>
          <v-col cols="12">
            <v-select
              outlined
              dense
              label="Equipo"
              :items="[]"
            ></v-select>
            <v-select
              :items="[
                'Fallas de firmware o del fabricante',
                'Falla electrónica o sobrevoltaje',
                'Falla mecánica o interna',
                'Errores físicos/ humanos',
              ]"
              outlined
              dense
              label="Problema"
            ></v-select>
          </v-col>
        </v-row>
      </div>
    </v-card-text>
    <v-card-actions class="justify-end"></v-card-actions>
  </v-card>
</template>
