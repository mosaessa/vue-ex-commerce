<template>
  <app-layout>
    <router-view />
    <QuickView />
    <v-snackbar
      color="green"
      v-model="bar"
      location="left bottom"
      timeout="3000"
      max-width="300"
      >{{ itemTitle }} has been added to your cart successfly!
      <template v-slot:actions>
        <v-icon @click="bar = false">mdi-close</v-icon>
      </template>
    </v-snackbar>
  </app-layout>
</template>
<script>
import AppLayout from "./components/global/AppLayout.vue";
import QuickView from "@/components/global/quick_view/QuickView.vue";

export default {
  inject: ["Emitter"],
  components: {
    AppLayout,
    QuickView,
  },
  data: () => ({
    bar: false,
    itemTitle: "",
  }),
  mounted() {
    this.Emitter.on("showMSG", (data) => {
      this.itemTitle = data;
      this.bar = true;
    });
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

input[type="number"]::-webkit-outer-spin-button,
input[type="number"]::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
</style>
