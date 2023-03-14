<template>
  <v-row>
    <v-col :cols="preview ? '8' : '12'">
      <v-card
        class="mt-5"
        width="100%"
        min-height="65vh"
        max-height="65vh"
        style="overflow-y: auto"
      >
        <h4 class="overline d-flex justify-center pt-5">
          Plantilla: {{ name || "sdas" }} <v-icon small>mdi-pencil</v-icon>
        </h4>
        <div class="container px-5">
          <div v-for="(section, indexSection) in sections" :key="indexSection">
            <div style=" d-flex flex-column align-center">
              <div class="d-flex">
                <h5 class="d-flex align-center">
                  <span>Sección:</span>
                  <v-text-field
                    v-model="section.nombre"
                    style="margin-top:0px; padding-left:5px; width='auto'"
                  ></v-text-field>
                </h5>
              </div>
              <v-row style="height: auto; border: 1px dotted">
                <v-col cols="12">
                  <div class="d-flex justify-end align-center">
                    <div class="d-flex mr-5">
                      <v-checkbox label="Lectura"></v-checkbox>
                      <v-checkbox label="Obligatorio"></v-checkbox>
                      <v-checkbox v-model="section.duplicable" label="Duplicable"></v-checkbox>
                    </div>
                    <v-btn
                      icon
                      @click="sections.splice(indexSection, 1)"
                      v-if="indexSection != 0"
                    >
                      <v-icon color="grey lighten-1">mdi-close</v-icon>
                    </v-btn>
                  </div>
                </v-col>
                <v-col cols="12">
                  <!-- <v-list subheader two-line>
                    <template v-for="(attribute, index) in section.attributes">
                      <v-list-item>
                        <v-list-item-avatar>
                          <v-icon class="grey lighten-1" dark>
                            mdi-arrow-right-bottom
                          </v-icon>
                        </v-list-item-avatar>

                        <v-list-item-content>
                          <v-list-item-title
                            class="overline"
                            v-text="attribute.name"
                          ></v-list-item-title>

                          <v-list-item-subtitle
                            class="overline"
                            v-text="`Tipo: ${attribute.componente.name}`"
                          ></v-list-item-subtitle>
                        </v-list-item-content>
                        <v-list-item-action>
                          <div class="d-flex justify-center">
                            <v-btn icon>
                              <v-icon color="grey lighten-1"
                                >mdi-pencil-outline</v-icon
                              >
                            </v-btn>
                            <v-btn icon>
                              <v-icon color="grey lighten-1"
                                >mdi-delete-empty</v-icon
                              >
                            </v-btn>
                          </div>
                        </v-list-item-action>
                      </v-list-item>
                      <v-divider inset></v-divider>
                    </template>
                  </v-list> -->
                  <v-treeview
                    activatable
                    :items="section.attributes"
                    item-text="name"
                  >
                    <template v-slot:prepend="{ open, item }">
                      <v-icon v-if="item.children.length">
                        {{ open ? "mdi-folder-open" : "mdi-folder" }}
                      </v-icon>
                      <v-icon v-else> mdi-vector-point </v-icon>
                    </template>
                    <template v-slot:label="{ item }">
                      <div class="d-flex justify-space-between align-center">
                        <div class="d-flex align-center">
                          <div class="d-flex align-center">
                            <h4>
                              {{ `${item.name}` }}
                            </h4>
                          </div>
                        </div>
                        <div class="d-flex">
                          <v-btn
                            icon
                            @click="openAttribute(indexSection, item)"
                          >
                            <v-icon color="grey lighten-1"
                              >mdi-file-tree</v-icon
                            >
                          </v-btn>
                          <v-btn icon>
                            <v-icon color="grey lighten-1"
                              >mdi-pencil-outline</v-icon
                            >
                          </v-btn>
                          <v-btn icon>
                            <v-icon color="grey lighten-1"
                              >mdi-delete-empty</v-icon
                            >
                          </v-btn>
                        </div>
                      </div>
                    </template>
                  </v-treeview>
                </v-col>
                <v-col cols="12">
                  <div class="d-flex justify-center">
                    <v-btn
                      class="ma-2 mx-5"
                      outlined
                      color="indigo"
                      @click="openAttribute(indexSection)"
                    >
                      AGREGAR REQUISITO
                    </v-btn>
                  </div>
                  <div></div>
                </v-col>
              </v-row>
            </div>
            <v-divider> </v-divider>
          </div>
          <v-btn
            class="mt-5"
            outlined
            color="indigo"
            @click="sections.push({ attributes: [] })"
          >
            NUEVA SECCIÓN
          </v-btn>
        </div>
        <div>
          <v-dialog
            v-model="atribute"
            transition="dialog-top-transition"
            max-width="600"
          >
            <Atribute @close="atribute = false" @add="addAttribute($event)" />
          </v-dialog>
        </div>
      </v-card>
    </v-col>
    <v-col cols="4" v-if="preview">
      <v-card class="mt-5" width="100%" min-height="65vh" max-height="65vh">
        <h4 class="overline d-flex justify-center pt-5">Vista Previa</h4>
        <v-row>
          <v-col cols="12" v-for="(section, index) in sections" :key="index">
            <div class="d-flex flex-column pa-4">
              <v-row class="d-flex justify-space-between align-center">
                <h4 class="overline">{{ section.nombre }}</h4>
                <div class="d-flex" v-if="section.duplicable">
                  <v-btn v-if="persona > 1" icon @click="personas -= 1">
                    <v-icon color="grey lighten-1">mdi-close</v-icon>
                  </v-btn>
                  <v-btn icon @click="sections.push(section)">
                    <v-icon color="grey lighten-1">mdi-plus</v-icon>
                  </v-btn>
                </div>
              </v-row>
              <div v-for="(attribute, i) in section.attributes" :key="i * 100">
                <component
                  :is="attribute.componente.tipo"
                  outlined
                  :label="attribute.name"
                  :items="attribute.options"
                  dense
                ></component>
              </div>
            </div>
          </v-col>
        </v-row>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
import Atribute from "@/components/Atribute";
import { VTextField } from "vuetify/lib/components/VTextField";
import { VSelect } from "vuetify/lib/components/VSelect";
export default {
  props: {
    name: String,
  },
  components: { Atribute, VTextField, VSelect },
  data() {
    return {
      atribute: false,
      sectionOpen: 0,
      attributeOpen: 0,
      preview: true,
      children: false,
      sections: [
        {
          attributes: [],
        },
      ],
    };
  },
  methods: {
    addAttribute(atribute) {
      this.atribute = false;
      if (this.attributeOpen >= 0) {
        this.sections[this.sectionOpen].attributes[
          this.attributeOpen
        ].children.push(Object.assign({ children: [] }, atribute));
      } else {
        this.sections[this.sectionOpen].attributes.push(
          Object.assign({ children: [] }, atribute)
        );
      }
    },
    openAttribute(section, attribute = null) {
      this.attributeOpen = this.sections[section].attributes.indexOf(attribute);
      this.sectionOpen = section;
      this.atribute = true;
    },

    nameAtributte(attribute) {
      this.$nextTick(() => {
        return attribute.componente.tipo;
      });
    },
  },
  watch: {
    sections() {
      console.log("0dasdas");
    },
  },
};
</script>
<style>
.input-template-name {
  margin-top: 20px !important;
}
.row {
  margin: 0px !important;
}
</style>
