<template>
  <div
    class="img-parent position-relative"
    style="height: 150px; overflow: hidden"
  >
    <v-hover v-slot="{ props, isHovering }">
      <img
        v-bind="props"
        :src="showenItem ? showenItem : image"
        class="w-100"
        :style="`height:100%;transition: 0.4s all ease-in-out;cursor: pointer;scale:${
          isHovering ? 1.05 : 1
        }`"
      />
      <v-btn
        height="30"
        class="bg-white quick-view-btn"
        :width="btnWidth"
        variant="outlined"
        style="
          text-transform: none;
          position: absolute;
          left: 50%;
          top: 50%;
          transform: translate(-50%, -50%);
          border-radius: 30px;
          font-size: 12px;
          transition: 0.2 all ease-in-out;
          opacity: 0;
        "
        @click="openQuickView(product)"
        >Quick View</v-btn
      >
    </v-hover>
  </div>
</template>
<script>
export default {
  inject: ["Emitter"],
  props: {
    image: {
      type: String,
    },
    showenItem: {
      type: String,
    },
    product: {
      type: Object,
    },
    btnWidth: {
      type: Number,
    },
  },
  methods: {
    openQuickView(product) {
      this.Emitter.emit("openQuickViewParent", product);
    },
  },
};
</script>
<style lang="scss">
.img-parent:hover {
  .quick-view-btn {
    opacity: 1 !important;
  }
}
</style>
