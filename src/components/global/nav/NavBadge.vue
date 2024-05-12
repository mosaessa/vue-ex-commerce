<template>
  <v-badge
    location="right top"
    :content="cartItems.length"
    v-if="cartItems.length"
    color="#205dc2"
    :offsetX="badgetSize ? badgetSize : '-14'"
  >
  </v-badge>
</template>
<script>
import { cartStroe } from "@/stores/cart";
import { mapState } from "pinia";
export default {
  computed: {
    ...mapState(cartStroe, ["cartItems"]),
  },
  props: {
    badgetSize: {
      type: Number,
    },
  },
};
</script>
