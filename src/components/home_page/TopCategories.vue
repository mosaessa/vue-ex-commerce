<template>
  <div class="top-cat">
    <div class="cyper-banner">
      <img src="@/assets/images/cyber-banner.webp" class="w-100" />
    </div>
    <div class="categories pt-13">
      <div class="title d-flex justify-center align-center px-5 mb-5">
        <h3 class="text-center flex-grow-1" style="font-weight: 900">
          Top Categories
        </h3>
        <!-- <a class="text-black" href="#">Shop All</a> -->
      </div>
      <v-container fuild>
        <v-row>
          <v-col
            cols="6"
            sm="4"
            md="3"
            lg="2"
            v-for="cat in categories"
            :key="cat.title"
          >
            <v-card
              class="text-center py-3 px-2"
              elevation="0"
              style="cursor: pointer"
            >
              <v-hover v-slot="{ props, isHovering }">
                <div
                  class="parent"
                  style="
                    overflow: hidden;
                    width: 100%;
                    height: 170px;
                    border-radius: 50%;
                  "
                >
                  <img
                    v-bind="props"
                    :src="cat.image"
                    :style="`width: 100%; height: 100%;transition: 0.4s all ease-in-out;cursor: pointer;scale:${
                      isHovering ? 1.05 : 1
                    }`"
                  />
                </div>
              </v-hover>
              <v-card-text>{{ cat.title }}</v-card-text>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </div>
  </div>
</template>
<script>
export default {
  data: () => ({
    categories: [
      {
        title: "Text Categories",
        image:
          "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTrSTstWSA1rO98kv-CRmlOo1xu6hJCxqmtqA&s",
      },
      {
        title: "Text Categories",
        image:
          "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTrSTstWSA1rO98kv-CRmlOo1xu6hJCxqmtqA&s",
      },
      {
        title: "Text Categories",
        image:
          "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTrSTstWSA1rO98kv-CRmlOo1xu6hJCxqmtqA&s",
      },
      {
        title: "Text Categories",
        image:
          "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTrSTstWSA1rO98kv-CRmlOo1xu6hJCxqmtqA&s",
      },
      {
        title: "Text Categories",
        image:
          "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTrSTstWSA1rO98kv-CRmlOo1xu6hJCxqmtqA&s",
      },
      {
        title: "Text Categories",
        image:
          "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTrSTstWSA1rO98kv-CRmlOo1xu6hJCxqmtqA&s",
      },
      {
        title: "Text Categories",
        image:
          "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTrSTstWSA1rO98kv-CRmlOo1xu6hJCxqmtqA&s",
      },
      {
        title: "Text Categories",
        image:
          "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTrSTstWSA1rO98kv-CRmlOo1xu6hJCxqmtqA&s",
      },
      {
        title: "Text Categories",
        image:
          "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTrSTstWSA1rO98kv-CRmlOo1xu6hJCxqmtqA&s",
      },
      {
        title: "Text Categories",
        image:
          "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTrSTstWSA1rO98kv-CRmlOo1xu6hJCxqmtqA&s",
      },
      {
        title: "Text Categories",
        image:
          "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTrSTstWSA1rO98kv-CRmlOo1xu6hJCxqmtqA&s",
      },

      {
        title: "Text Categories",
        image:
          "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTrSTstWSA1rO98kv-CRmlOo1xu6hJCxqmtqA&s",
      },
    ],
  }),
};
</script>
