<template>
  <v-app>
    <v-app-bar
      app
      color="white"
      dark
    >
      <div class="d-flex align-center">


        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="@/assets/logo.png"
          width="150"
        />
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
        color="black"
        text
      >
        <span class="mr-2">Main Page</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <DataList />
    </v-main>
  </v-app>
</template>

<script>
import DataList from './components/DataList';

export default {
  name: 'App',

  components: {
    DataList,
  },

  data: () => ({
    //
  }),
};
</script>
