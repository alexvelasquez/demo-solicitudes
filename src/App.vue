<template>
  <v-app>
    <v-bottom-navigation v-model="value" color="indigo">
      <v-btn class="btn-nav" value="recent" to="/">
        <span>SOLICITUDES</span>

        <v-icon>mdi-list-box-outline</v-icon>
      </v-btn>

      <v-btn class="btn-nav" value="favorites" to="/nueva-plantilla">
        <span>NUEVA PLANTILLA</span>

        <v-icon>mdi-file-document-plus-outline</v-icon>
      </v-btn>
    </v-bottom-navigation>

    <!-- Sizes your content based upon application components -->
    <v-main>
      <!-- Provides the application the proper gutter -->
      <v-container fluid>
        <!-- If using vue-router -->
        <router-view></router-view>
      </v-container>
    </v-main>

    <v-footer app>
      <!-- -->
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: "App",

  data: () => ({
    value: 0,
  }),
};
</script>
<style>
v-main {
  background-color: #F5F5F5
}
.btn-nav:not(.v-btn--round).v-size--default {
  height: auto !important;
}

.theme--light.v-btn.v-btn--has-bg {
    background-color: transparent !important;
}

.swal2-popup {
font-family: 'Roboto' !important;
}
</style>
