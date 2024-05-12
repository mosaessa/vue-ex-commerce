<template>
  <div class="top-offers bg-grey-lighten-4 py-9">
    <v-container fluid>
      <v-row>
        <v-col
          cols="12"
          sm="4"
          md="4"
          lg="4"
          class="pr-lg-6"
          style="height: 270px"
        >
          <v-hover v-slot="{ isHovering, props }">
            <div
              class="parent"
              v-bind="props"
              style="overflow: hidden; height: 100%; border-radius: 7px"
            >
              <img
                :style="`height:100%;transition: 0.4s all ease-in-out;cursor: pointer;width:100%;scale:${
                  isHovering ? 1.05 : 1
                }`"
                src="@/assets/images/playstations.webp"
              />
            </div>
          </v-hover>
        </v-col>
        <v-col
          cols="12"
          sm="4"
          md="4"
          lg="4"
          class="pr-lg-6"
          style="height: 270px"
        >
          <v-hover v-slot="{ isHovering, props }">
            <div
              class="parent"
              v-bind="props"
              style="overflow: hidden; height: 100%; border-radius: 7px"
            >
              <img
                :style="`height:100%;transition: 0.4s all ease-in-out;cursor: pointer;width:100%;scale:${
                  isHovering ? 1.05 : 1
                }`"
                src="@/assets/images/headset.webp"
              />
            </div>
          </v-hover>
        </v-col>
        <v-col
          cols="12"
          sm="4"
          md="4"
          lg="4"
          class="pr-lg-6"
          style="height: 270px"
        >
          <v-hover v-slot="{ isHovering, props }">
            <div
              class="parent"
              v-bind="props"
              style="overflow: hidden; height: 100%; border-radius: 7px"
            >
              <img
                :style="`height:100%;transition: 0.4s all ease-in-out;cursor: pointer;width:100%;scale:${
                  isHovering ? 1.05 : 1
                }`"
                src="@/assets/images/chairs.webp"
              />
            </div>
          </v-hover>
        </v-col>
      </v-row>
      <v-row class="mt-9">
        <v-col cols="12" sm="6" class="mt-3 px-3 py-0 pl-sm-5">
          <v-hover v-slot="{ isHovering, props }">
            <div
              class="parent"
              v-bind="props"
              style="overflow: hidden; height: 100%; border-radius: 7px"
            >
              <img
                :style="`height:100%;transition: 0.4s all ease-in-out;cursor: pointer;width:100%;scale:${
                  isHovering ? 1.05 : 1
                }`"
                src="@/assets/images/iphones.webp"
              />
            </div>
          </v-hover>
        </v-col>
        <v-col cols="12" sm="6" class="mt-3 px-3 py-0 pr-sm-5">
          <v-hover v-slot="{ isHovering, props }">
            <div
              class="parent"
              v-bind="props"
              style="overflow: hidden; height: 100%; border-radius: 7px"
            >
              <img
                :style="`height:100%;transition: 0.4s all ease-in-out;cursor: pointer;width:100%;scale:${
                  isHovering ? 1.05 : 1
                }`"
                src="@/assets/images/laptops.webp"
              />
            </div>
          </v-hover>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>
