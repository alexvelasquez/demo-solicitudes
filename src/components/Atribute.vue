<template>
  <v-card>
    <v-toolbar color="primary" dark>Nuevo requisito</v-toolbar>
    <v-card-text>
      <v-row>
        <v-col cols="12">
          <div class="d-flex justify-end">
            <v-checkbox label="Lectura" value="John"></v-checkbox>
            <v-checkbox label="Obligatorio" value="John"></v-checkbox>
            <v-checkbox label="Duplicable" value="John"></v-checkbox>
          </div>
        </v-col>
        <v-col cols="12">
          <v-text-field
            v-model="attribute.name"
            label="Nombre"
            dense
            outlined
          ></v-text-field>
        </v-col>
        <v-col class="mt-n8">
          <v-select
            v-model="attribute.codigo"
            :items="['COD. RECURSOS EQUIPAMIENTO', 'COD. VERIFICACIÓN CUIT/CUIL', 'COD. ROLES USUARIO']"
            label="Código"
            dense
            outlined
          >
          </v-select>
        </v-col>
        <v-col cols="12" class="mt-n8">
          <v-select
            v-model="attribute.componente"
            label="Tipo"
            dense
            item-text="name"
            return-object
            outlined
            :items="[
              { id: 'NUMERO', name: 'Número', tipo: 'VTextField' },
              { id: 'FECHA', name: 'Fecha' },
              {
                id: 'TEXT_CORTO',
                name: 'Texto Corto',
                nameType: 'Input',
                tipo: 'VTextField',
              },
              {
                id: 'TEXT_LARGO',
                name: 'Texto Largo',
                nameType: 'Text Area',
              },
              {
                id: 'LISTA_LARGA',
                name: 'Lista Larga',
                nameType: 'Select',
                tipo: 'VSelect',
              },
              {
                id: 'LISTA_CORTA',
                name: 'Lista Corta',
                nameType: 'Radio Button',
              },
              {
                id: 'LISTA_MULTIPLE',
                name: 'Lista Múltiple',
                nameType: 'checkboxs',
              },
            ]"
            persistent-hint
            :hint="
              attributeComponente == 'LISTA_LARGA'
                ? '<a>Agregar Opción</a>'
                : ''
            "
          >
            <template v-slot:message="{ message }">
              <span v-html="message" @click="options.push({})"></span>
            </template>
            <template v-slot:item="{ item }">
              <span
                style="font-size: 0.83em; font-weight: 500; line-height: 1rem"
              >
                {{ item.name }}
                {{ item.nameType ? ` (${item.nameType}) ` : "" }}
              </span>
            </template>
          </v-select>
        </v-col>

        <v-col cols="12">
          <v-row
            v-for="(option, index) in options"
            :key="index"
            class="d-flex mt-n10 justify-center align-center"
          >
            <v-col cols="12" md="10">
              <v-text-field v-model="option.valor" label="valor"></v-text-field>
            </v-col>
            <v-col cols="12" md="2">
              <div class="d-flex">
                <v-btn
                  text
                  icon
                  @click="attribute.options.push(option.valor)"
                  :class="{
                    'd-none': attribute.options.includes(option.valor),
                  }"
                >
                  <v-icon>mdi-check-bold</v-icon>
                </v-btn>
                <v-btn text icon @click="options.splice(index, 1)">
                  <v-icon>mdi-close-thick</v-icon>
                </v-btn>
              </div>
            </v-col>
          </v-row>
        </v-col>
        <v-col cols="12" class="mt-n10">
          <v-checkbox
            v-model="externo"
            :label="`¿Requiere recurso externo?`"
          ></v-checkbox>
        </v-col>

        <v-col cols="12" v-if="externo" class="p-0">
          <v-row class="m-0">
            <v-col cols="12" class="mt-n10 p-0">
              <v-text-field label="Url" dense outlined></v-text-field>
            </v-col>
            <v-col cols="12" class="mt-n10 p-0">
              <v-text-field
                label="Campo identificador"
                dense
                outlined
              ></v-text-field>
            </v-col>
            <v-col cols="12" class="mt-n10 p-0">
              <v-text-field
                label="Campo etiqueta"
                dense
                outlined
              ></v-text-field>
            </v-col>
          </v-row>
        </v-col>
      </v-row>
    </v-card-text>
    <v-card-actions class="justify-end">
      <v-btn text @click="$emit('close')">Cerrar</v-btn>
      <v-btn text @click="save()">Guardar</v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  data() {
    return {
      options: [],
      componente: null,
      externo: false,
      attribute: {
        name: "",
        codigo: null,
        componente: null,
        options: [],
      },
    };
  },
  methods: {
    save() {
      const value = Object.assign({}, this.attribute);
      this.attribute = Object.assign(
        {},
        {
          name: "",
          codigo: "",
          componente: null,
          options: [],
        }
      );
      this.$emit("add", value);
    },
  },
  computed: {
    attributeComponente() {
      return this.attribute.componente ? this.attribute.componente.id : null;
    },
  },
};
</script>
