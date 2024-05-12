<template>
  <div class="new-products pt-9">
    <v-container fluid>
      <div class="title mb-2 px-5 d-flex align-center justify-space-between">
        <h2 style="font-weight: 900; font-size: 30px">New Products</h2>
        <a href="#" class="text-black" style="font-size: 14px">Shop All</a>
      </div>
      <v-row>
        <v-col class="pt-12" cols="7" v-if="!products.length">
          <v-row>
            <v-col cols="4" v-for="num in 3" :key="num">
              <v-skeleton-loader
                type="image, article, button"
              ></v-skeleton-loader>
            </v-col>
          </v-row>
        </v-col>
        <v-col cols="12" md="7" sm="12" class="pt-12 order-1 order-md-0" v-else>
          <Swiper
            :pagination="{ el: '.swiper-pagination', clickable: true }"
            :modules="modules"
            :slides-per-view="2"
            :space-between="20"
            :autoplay="{ delay: 2000 }"
            :breakpoints="breakpoints"
            class="pb-9 px-5"
          >
            <swiper-slide v-for="item in products" :key="item.id">
              <v-card elevation="0" class="pb-5">
                <v-hover v-slot="{ props, isHovering }">
                  <div
                    class="img-parent position-relative"
                    style="height: 150px; overflow: hidden"
                  >
                    <img
                      v-bind="props"
                      :src="
                        showenItem[item.title]
                          ? showenItem[item.title]
                          : item.thumbnail
                      "
                      class="w-100"
                      :style="`height:100%;transition: 0.4s all ease-in-out;cursor: pointer;scale:${
                        isHovering ? 1.05 : 1
                      }`"
                    />
                    <v-btn
                      height="30"
                      class="bg-white quick-view-btn"
                      width="60"
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
                      @click="openQuickView(item)"
                      >Quick View</v-btn
                    >
                  </div>
                </v-hover>
                <v-card-text class="pl-0">
                  {{
                    `(${item.title})${item.description}`.length <= 40
                      ? `(${item.title}) ${item.description}`
                      : `(${item.title}) ${item.description}`.substring(0, 40) +
                        "..."
                  }}
                </v-card-text>
                <v-rating
                  v-model="item.rating"
                  half-increments
                  readonly
                  color="yellow-darken-2"
                  size="small"
                  density="compact"
                ></v-rating>
                <v-card-text class="pl-0">
                  <del class="text-red">${{ item.price }}</del> From
                  <span class="text-green" style="font-weight: 900"
                    >${{
                      Math.ceil(
                        item.price -
                          item.price * (item.discountPercentage / 100)
                      )
                    }}</span
                  >
                </v-card-text>
                <Swiper
                  :modules="modules"
                  :slides-per-view="3"
                  :space-between="10"
                >
                  <swiper-slide v-for="(pic, i) in item.images" :key="i">
                    <v-btn-toggle class="px-5" v-model="showenItem[item.title]">
                      <v-btn
                        :value="pic"
                        size="x-small"
                        rounded="s"
                        color="rgb(243 233 233)"
                        :ripple="false"
                      >
                        <img
                          style="border-radius: 10%; border: 1px solid black"
                          :src="pic"
                          width="50"
                          height="30"
                        />
                      </v-btn>
                    </v-btn-toggle>
                  </swiper-slide>
                  <div class="swiper-pagination"></div>
                </Swiper>
                <div class="my-5 text-center">
                  <v-btn
                    density="compact"
                    class="py-2 px-12"
                    style="text-transform: none; border-radius: 10px"
                    variant="outlined"
                    @click="
                      $router.push({
                        name: 'products_detalis',
                        params: { productId: item.id },
                      })
                    "
                  >
                    Choose Opstions
                  </v-btn>
                </div>
              </v-card>
            </swiper-slide>
            <div class="swiper-pagination"></div>
          </Swiper>
        </v-col>
        <v-col cols="12" md="5" lg="5" sm="12">
          <img src="@/assets/images/vr-banner.webp" class="w-100" />
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>
<script>
import { Swiper, SwiperSlide } from "vue-awesome-swiper";
import { Pagination } from "swiper";
import { VSkeletonLoader } from "vuetify/lib/labs/components.mjs";
export default {
  inject: ["Emitter"],
  components: {
    Swiper,
    SwiperSlide,
    VSkeletonLoader,
  },
  data: () => ({
    showenItem: {},
    modules: [Pagination],
    breakpoints: {
      0: {
        slidesPerView: 1,
      },
      580: {
        slidesPerView: 2,
      },
      // 1024: {
      //   slidesPerView: 3,
      // },
    },
  }),
  props: {
    products: {
      type: Array,
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
.new-products {
  .img-parent:hover {
    .quick-view-btn {
      opacity: 1 !important;
    }
  }
}
</style>
