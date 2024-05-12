<template>
  <div class="quick-view mt-16">
    <v-dialog v-model="dialog" max-width="900" max-height="600">
      <v-icon
        @click="dialog = false"
        style="
          position: absolute;
          right: -14px;
          /* top: -5px; */
          background-color: black;
          color: rgb(198, 198, 198);
          font-size: 18px;
          padding: 13px;
          z-index: 10;
        "
        >mdi-close</v-icon
      >
      <v-card elevation="0" class="content-card">
        <v-container fluid class="bg-white pt-10 px-10">
          <v-row>
            <v-col cols="12" md="7">
              <img
                :src="tab ? tab : product.thumbnail"
                class="w-100"
                height="400"
                v-if="!loading"
              />
              <v-skeleton-loader
                v-if="loading"
                type="image, image, image"
              ></v-skeleton-loader>
              <v-tabs
                v-if="!loading"
                center-active
                height="130"
                v-model="tab"
                class="mt-10"
              >
                <v-tab v-for="(img, i) in product.images" :key="i" :value="img">
                  <img :src="img" height="70" width="100" class="mx-10" />
                </v-tab>
              </v-tabs>
            </v-col>
            <v-col cols="12" md="5" class="pt-0 pl-6">
              <v-skeleton-loader
                v-if="loading"
                type="article, article"
              ></v-skeleton-loader>
              <v-card elevation="0" v-if="!loading">
                <v-card-title
                  class="px-0"
                  style="
                    font-size: 19px;
                    font-weight: bold;
                    white-space: pre-wrap;
                  "
                >
                  ({{ product.title }}) Sample - {{ product.category }}
                </v-card-title>
                <div class="rating-paret d-flex align-center" style="gap: 10px">
                  <v-rating
                    v-model="product.rating"
                    half-increments
                    readonly
                    color="yellow-darken-2"
                    size="small"
                    density="compact"
                  ></v-rating>
                  <span
                    class="mt-1"
                    style="font-size: 13px; color: rgb(96, 96, 96)"
                    >Stock: {{ product.stock }}</span
                  >
                </div>
                <v-card-text
                  class="px-0 mt-5 mt-md-0"
                  style="font-size: 14px; color: rgb(96, 96, 96)"
                >
                  {{ product.description }}
                </v-card-text>
                <v-card-text
                  class="px-0 pt-0"
                  style="font-size: 14px; color: rgb(96, 96, 96)"
                >
                  Brand: {{ product.brand }}
                </v-card-text>
                <v-card-text
                  class="px-0 pt-0"
                  style="font-size: 14px; color: rgb(96, 96, 96)"
                >
                  Availabilty:
                  {{ product.stock > 0 ? "In Stock" : "Out Of Stock" }}
                </v-card-text>
                <v-card-text class="px-0 pt-0" style="font-size: 16px">
                  <del class="text-red">${{ product.price }}</del> From
                  <span class="text-green" style="font-weight: 900"
                    >${{
                      Math.ceil(
                        product.price -
                          product.price * (product.discountPercentage / 100)
                      )
                    }}</span
                  >
                </v-card-text>
                <v-card-text class="px-0"> Quantity </v-card-text>
                <div
                  class="counter px-1"
                  style="
                    border: 1px solid rgb(201, 201, 201);
                    width: fit-content;
                    border-radius: 30px;
                  "
                >
                  <v-icon @click="quantity > 1 ? quantity-- : false" size="22"
                    >mdi-minus</v-icon
                  >
                  <input
                    class="text-center py-2"
                    type="number"
                    style="
                      border: none;
                      outline: none;
                      width: 60px;
                      font-size: 13px;
                    "
                    min="1"
                    v-model="quantity"
                  />
                  <v-icon @click="quantity++" size="22">mdi-plus</v-icon>
                </div>
                <v-card-text class="px-0">
                  Subtotal: ${{
                    quantity *
                    Math.ceil(
                      product.price -
                        product.price * (product.discountPercentage / 100)
                    )
                  }}</v-card-text
                >
                <v-card-actions class="mt-2 w-100 px-0">
                  <v-btn
                    variant="outlined"
                    height="50"
                    density="compact"
                    class="w-75 text-white"
                    style="
                      text-transform: none;
                      border-radius: 30px;
                      background-color: rgb(20, 20, 20);
                    "
                    @click="addToCart(product)"
                    :loading="btnLoading"
                    >Add To Cart
                  </v-btn>
                </v-card-actions>
              </v-card>
            </v-col>
          </v-row>
        </v-container>
      </v-card>
    </v-dialog>
  </div>
</template>
<script>
import { cartStroe } from "@/stores/cart";
import { mapActions } from "pinia";
export default {
  inject: ["Emitter"],
  data: () => ({
    loading: false,
    tab: "",
    quantity: 1,
    dialog: false,
    product: "",
    btnLoading: false,
  }),
  mounted() {
    this.Emitter.on("openQuickViewParent", (data) => {
      this.quantity = 1;
      this.loading = true;
      this.product = data;
      this.dialog = true;
      setTimeout(() => {
        this.loading = false;
      }, 300);
    });
  },
  methods: {
    ...mapActions(cartStroe, ["addItem"]),
    addToCart(item) {
      item.quantity = this.quantity;
      this.btnLoading = true;
      setTimeout(() => {
        this.btnLoading = false;
        this.Emitter.emit("openCart");
        this.Emitter.emit("showMSG", item.title);
        this.dialog = false;
      }, 500);
      this.addItem(item);
    },
  },
};
</script>
<style lang="scss">
.content-card {
  &::-webkit-scrollbar {
    width: 5px;
  }
  &::-webkit-scrollbar-thumb {
    width: 5px;
    background-color: rgb(150, 150, 150);
  }
  &::-webkit-scrollbar-track {
    width: 5px;
    background-color: rgb(200, 200, 200);
  }
}
</style>
