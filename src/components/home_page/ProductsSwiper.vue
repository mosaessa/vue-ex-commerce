<template>
  <div class="products-swiper py-7">
    <div class="title mb-10 px-5 d-flex align-center justify-space-between">
      <h2
        style="font-weight: 900; font-size: 30px"
        :class="[`text-${titleColor}`]"
      >
        {{ title }}
      </h2>
      <a href="#" class="text-black" style="font-size: 14px">Shop All</a>
    </div>
    <v-container fluid v-if="!products.length">
      <v-row>
        <v-col class="pb-9 px-5" cols="12">
          <v-row>
            <v-col cols="3" v-for="num in 4" :key="num">
              <v-skeleton-loader
                type="image, article, button"
              ></v-skeleton-loader>
            </v-col>
          </v-row>
        </v-col>
      </v-row>
    </v-container>
    <Swiper
      :pagination="{ el: '.swiper-pagination', clickable: true }"
      :modules="modules"
      :slides-per-view="4"
      :space-between="35"
      :navigation="{ prevIcon: '.swiper-prev', nextIcon: '.swiper-next' }"
      :autoplay="{
        delay: 2000,
        pauseOnMouseEnter: true,
        disableOnInteraction: false,
      }"
      :loop="true"
      :breakpoints="breakpoints"
      class="pb-9 px-5"
    >
      <swiper-slide v-for="item in products" :key="item.id">
        <v-card elevation="0" class="pb-5">
          <v-hover v-slot="{ props, isHovering }">
            <div
              class="img-parent position-relative"
              style="height: 200px; overflow: hidden"
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
              `(${item.title})${item.description}`.length <= 57
                ? `(${item.title}) ${item.description}`
                : `(${item.title}) ${item.description}`.substring(0, 57) + "..."
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
                  item.price - item.price * (item.discountPercentage / 100)
                )
              }}</span
            >
          </v-card-text>
          <v-btn-toggle v-model="showenItem[item.title]" mandatory>
            <v-btn
              v-for="(pic, i) in item.images"
              :value="pic"
              :key="i"
              size="x-small"
              rounded="xl"
              color="#8b8181"
              :ripple="false"
            >
              <img
                style="border-radius: 50%; border: 1px solid black"
                :src="pic"
                width="50"
                height="30"
              />
            </v-btn>
          </v-btn-toggle>
          <div class="my-5 text-center">
            <v-btn
              density="compact"
              class="py-2 px-12"
              style="text-transform: none; border-radius: 30px"
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
      <div class="swiper-prev"></div>
      <div class="swiper-next"></div>
      <div class="swiper-pagination"></div>
    </Swiper>
  </div>
</template>
<script>
import { Swiper, SwiperSlide } from "vue-awesome-swiper";
import { Pagination, Navigation, Autoplay } from "swiper";
export default {
  inject: ["Emitter"],
  methods: {
    openQuickView(product) {
      this.Emitter.emit("openQuickViewParent", product);
    },
  },
  components: {
    Swiper,
    SwiperSlide,
  },
  data: () => ({
    showenItem: {},
    modules: [Pagination, Navigation, Autoplay],
    breakpoints: {
      0: {
        slidesPerView: 1,
      },
      580: {
        slidesPerView: 2,
      },
      767: {
        slidesPerView: 3,
      },
      990: {
        slidesPerView: 4,
      },
    },
  }),
  props: {
    products: {
      type: Array,
    },
    title: {
      type: String,
    },
    titleColor: {
      type: String,
    },
  },
};
</script>
<style lang="scss">
.products-swiper {
  .swiper-button-next,
  .swiper-button-prev {
    width: 35px;
    height: 35px;
    border: 2px solid rgb(95, 95, 95);
    border-radius: 50%;
    background-color: white;
    top: 41%;
    &::after {
      font-size: 13px;
      padding: 0;
      display: flex;
      font-weight: 900;
      color: rgb(95, 95, 95);
    }
  }
  .swiper-pagination-bullet {
    width: 12px;
    height: 12px;
  }
  .img-parent:hover {
    .quick-view-btn {
      opacity: 1 !important;
    }
  }
}
// Media Query
@media (max-width: 580px) {
  .products-swiper {
    .img-parent {
      height: 250px !important;
    }
    .swiper-button-next,
    .swiper-button-prev {
      top: 44%;
    }
  }
}
</style>
