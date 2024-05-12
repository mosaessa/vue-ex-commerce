<template>
  <div class="shop-withus py-14">
    <div class="title">
      <h2 class="text-center mb-5"><span>Why Shop</span> With Us?</h2>
    </div>
    <v-container fluid>
      <v-row>
        <v-col
          cols="12"
          sm="6"
          md="3"
          v-for="item in ourInfo"
          :key="item.title"
          class="px-1 mb-4 mb-lg-0"
        >
          <v-card
            elevation="0"
            class="text-center text-white"
            color="transparent"
          >
            <div class="img-parent">
              <img :src="item.image" />
            </div>
            <v-card-title class="card-title">
              {{ item.title }}
            </v-card-title>
            <v-card-text class="pb-0"> {{ item.desc }}</v-card-text>
            <a href="#" class="text-white">Learn More</a>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>
<script>
export default {
  data: () => ({
    ourInfo: [
      {
        title: "Free Shipping On First Order",
        desc: "Lorem ipsum dolor sit amet consectetur",
        image: require("@/assets/images/free-shipping.png"),
      },
      {
        title: "Weekly Flash Sale",
        desc: "Lorem ipsum dolor sit amet consectetur",
        image: require("@/assets/images/weekly-flash-sales.png"),
      },
      {
        title: "Anual Payment Discount",
        desc: "Lorem ipsum dolor sit amet consectetur",
        image: require("@/assets/images/discount.png"),
      },
      {
        title: "Cachback Reward Program",
        desc: "Lorem ipsum dolor sit amet consectetur",
        image: require("@/assets/images/cash-back.png"),
      },
    ],
  }),
};
</script>

<style lang="scss">
.shop-withus {
  background-image: url(../../assets/images/why-shop-with-us-banner.webp);
  background-repeat: repeat-x;
  background-size: cover;
  h2 {
    color: white;
    font-size: 45;
    font-weight: 900;
    span {
      color: rgb(45, 251, 223);
    }
  }
  .card-title {
    white-space: pre-wrap;
    line-height: 1.2;
    font-weight: 700;
  }
  a {
    font-weight: 700;
    font-size: 14px;
  }
}
</style>
