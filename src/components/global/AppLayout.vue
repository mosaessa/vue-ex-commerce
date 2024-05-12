<template>
  <div class="layout">
    <v-layout class="position-relative">
      <!-- <v-layout> -->
      <CartDrawer :windowWidth="windowWidth" />
      <MenuDrawer :windowWidth="windowWidth" />
      <!-- <v-main style="padding-top: 150px"> -->
      <v-main
        :style="`padding-top: ${
          $route.name == 'check_out'
            ? '0px'
            : windowWidth <= 990
            ? '60px'
            : '150px'
        }`"
      >
        <!-- <v-main :style="`padding-top:  150px`"> -->
        <slot></slot>
      </v-main>
      <AppNav
        v-show="$route.name != 'check_out' && !showFixed && windowWidth > 990"
      />
      <ResponsiveNav
        v-show="windowWidth <= 990 && $route.name != 'check_out'"
      />
      <FixedNav
        v-show="$route.name != 'check_out' && showFixed && windowWidth > 990"
      />
      <AppFooter v-if="$route.name != 'check_out'" />
    </v-layout>
  </div>
</template>

<script>
import AppNav from "./AppNav.vue";
import AppFooter from "./AppFooter.vue";
import CartDrawer from "./CartDrawer.vue";
import FixedNav from "./FixedNav.vue";
import ResponsiveNav from "./ResponsiveNav.vue";
import MenuDrawer from "./MenuDrawer.vue";
export default {
  data: () => ({
    drawer: false,
    windowWidth: 0,
    showFixed: false,
  }),
  components: {
    AppNav,
    AppFooter,
    CartDrawer,
    FixedNav,
    ResponsiveNav,
    MenuDrawer,
  },
  mounted() {
    this.windowWidth = window.innerWidth;
    window.onresize = () => {
      this.windowWidth = window.innerWidth;
    };
    window.onscroll = () => {
      if (window.scrollY >= 250) {
        this.showFixed = true;
      } else {
        this.showFixed = false;
      }
    };
  },
};
</script>
