<template>
  <div class="container">
    <div
      v-if="!template"
      class="d-flex justify-center align-center"
      style="height: 80vh"
    >
      <v-btn class="ma-2" outlined color="indigo" @click="newTemplate()">
        NUEVA PLANTILLA
      </v-btn>
    </div>

    <div v-if="template">
      <Template :name="name"></Template>
    </div>
  </div>
</template>

<script>
import Template from "@/components/Template";
export default {
  name: "Home",
  components: { Template },
  data() {
    return {
      template: false,
      name: "",
    };
  },
  methods: {
    async newTemplate() {
      const response = await this.$swal({
        icon: "info",
        title: "Plantilla",
        text: "Ingrese un nombre",
        input: "text",
        showClass: {
          popup: "font-sans",
        },
      });
      this.name = response.value;
      this.template = true;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.font-sans {
  font-family: sans-serif;
}
</style>
