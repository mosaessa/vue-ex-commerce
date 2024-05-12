<template>
  <div class="products-category mt-10">
    <h1 class="text-center">{{ $route.query.title }}</h1>
    <v-container>
      <!-- <v-card
        :loading="loading"
        class="mt-5"
        elevation="0"
        style="min-height: 350px"
      > -->
      <v-card class="mt-5" elevation="0" style="min-height: 350px">
        <v-row>
          <v-col cols="12">
            <v-row v-if="loading">
              <v-col cols="12" sm="6" md="4" lg="3" v-for="num in 4" :key="num">
                <v-skeleton-loader
                  type="image, article, button"
                ></v-skeleton-loader>
              </v-col>
            </v-row>
          </v-col>
        </v-row>
        <v-row v-if="!loading">
          <v-col
            cols="12"
            sm="6"
            md="4"
            lg="3"
            v-for="item in categoryProducts.products"
            :key="item.id"
            class="px-5"
          >
            <v-lazy>
              <v-card elevation="0" class="pb-5">
                <ImgBtnQuickView
                  :image="item.thumbnail"
                  :showenItem="showenItem[item.title]"
                  :product="item"
                  :btnWidth="90"
                />

                <v-card-text class="pl-0">
                  {{
                    `(${item.title})${item.description}`.length <= 57
                      ? `(${item.title}) ${item.description}`
                      : `(${item.title}) ${item.description}`.substring(0, 57) +
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
                <v-btn-toggle v-model="showenItem[item.title]">
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
                    height="35"
                    width="220"
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
            </v-lazy>
          </v-col>
        </v-row>
      </v-card>
    </v-container>
  </div>
</template>
<script>
import { mapActions, mapState } from "pinia";
import { productsModule } from "@/stores/products";
import { VSkeletonLoader } from "vuetify/lib/labs/components.mjs";
import ImgBtnQuickView from "@/components/global/quick_view/ImgBtnQuickView.vue";
export default {
  components: {
    VSkeletonLoader,
    ImgBtnQuickView,
  },
  data: () => ({
    showenItem: {},
    loading: false,
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
  methods: {
    ...mapActions(productsModule, ["getProductsByCategory"]),
  },
  computed: {
    ...mapState(productsModule, ["categoryProducts"]),
  },
  watch: {
    async $route() {
      if (this.$route.name == "products_category") {
        document.documentElement.scrollTo(0, 0);
        this.loading = true;
        await this.getProductsByCategory(this.$route.query.category);
        this.loading = false;
      }
    },
  },
  async mounted() {
    if (!this.$route.query.category) {
      return this.$router.go(-1);
    }
    this.loading = true;
    await this.getProductsByCategory(this.$route.query.category);
    this.loading = false;
  },
};
</script>
