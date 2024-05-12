<template>
  <ul class="d-flex justify-space-between" style="list-style: none">
    <li v-for="category in categories" :key="category">
      <router-link
        :to="{
          name: 'products_category',
          query: { category: category.route, title: category.title },
        }"
        style="text-decoration: none; color: white"
      >
        {{ category.title }}
      </router-link>
    </li>
  </ul>
</template>
<script>
import { productsModule } from "@/stores/products";
import { mapState } from "pinia";
export default {
  inject: ["Emitter"],
  methods: {
    openCart() {
      this.Emitter.emit("openCart");
    },
  },

  computed: {
    ...mapState(productsModule, ["categories"]),
  },
};
</script>
