<template>
  <div class="home">
    <UpperBannerVue />
    <TheFeatures style="padding: 36px 0 36px 0" />
    <TopOffers />
    <ProdcutsComponent
      :products="flashDeals"
      title="Flash Deals"
      titleColor="red"
    />
    <TopCategories />
    <NewProdcus :products="newProducts" />
    <QualityFeatures />
    <ProdcutsComponent
      :products="mobilePhones"
      title="Top Mobile Phones"
      titleColor="black"
    />
    <BandCover />
    <ProdcutsComponent
      :products="fragrances"
      title="Top Fragrances"
      titleColor="purple"
    />
    <MiddleBanner />
    <ProdcutsComponent
      :products="groceries"
      title="Top Groceries"
      titleColor="red"
    />
    <WhyShopWithUs />
  </div>
</template>
<script>
import UpperBannerVue from "@/components/home_page/UpperBanner.vue";
import TheFeatures from "@/components/home_page/TheFeatures.vue";
import TopOffers from "@/components/home_page/TopOffers.vue";
import TopCategories from "@/components/home_page/TopCategories.vue";
import ProdcutsComponent from "@/components/home_page/ProductsSwiper.vue";
import NewProdcus from "@/components/home_page/NewProdcus.vue";
import QualityFeatures from "@/components/home_page/QualityFeatures.vue";
import BandCover from "@/components/home_page/BandCover.vue";
import MiddleBanner from "@/components/home_page/MiddleBanner.vue";
import WhyShopWithUs from "@/components/home_page/WhyShopWithUs.vue";
import { productsModule } from "@/stores/products";
import { mapActions, mapState } from "pinia";
export default {
  components: {
    UpperBannerVue,
    TheFeatures,
    TopOffers,
    ProdcutsComponent,
    TopCategories,
    NewProdcus,
    QualityFeatures,
    BandCover,
    MiddleBanner,
    WhyShopWithUs,
  },
  computed: {
    ...mapState(productsModule, [
      "flashDeals",
      "newProducts",
      "mobilePhones",
      "fragrances",
      "groceries",
    ]),
  },
  methods: {
    ...mapActions(productsModule, ["getProducts"]),
  },
  async mounted() {
    await this.getProducts();
  },
};
</script>
