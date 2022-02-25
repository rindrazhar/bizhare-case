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

    <v-main> </v-main>
  </v-app>
</template>

<script>
import axios from "axios";

export default {
  name: "App",

  data() {
    return {
      resultsData: [],
      categoryData: [],
    };
  },
  methods: {
    getData() {
      const item = JSON.stringify({
        size: 0,
        page: 0,
        listCategory: [],
      });
      axios
        .post("http://sandbox.bizharedev.id:17001/business/parent/all", item, {
          headers: {
            "content-type": "application/json",
          },
        })
        .then((res) => {
          this.resultsData = res.data.data;
          console.log("data", this.resultsData);
        });
    },

    getCategory() {
      axios
        .get("http://sandbox.bizharedev.id:17001/media/param/business/category")
        .then((res) => {
          this.categoryData = res.data.data;
          console.log("data", this.categoryData);
        });
    },

    created() {
      this.getData();
      this.getCategory();
    },
  },
};
</script>
