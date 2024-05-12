<template>
  <div class="order-success">
    <v-dialog v-model="dialog" width="50%" persistent>
      <v-container>
        <v-row>
          <v-col cols="12">
            <v-card class="text-center py-7">
              <div class="text--center">
                <v-icon
                  style="
                    color: green;
                    background-color: white;
                    font-size: 76px;
                    border-radius: 50%;
                    width: 100px;
                    height: 100px;
                    border: 1px solid green;
                  "
                  >mdi-check</v-icon
                >
              </div>
              <v-card-title
                style="
                  font-size: 30px;
                  font-weight: bold;
                  color: rgb(93, 93, 93);
                "
              >
                Order Placed Successfly
              </v-card-title>
              <v-card-text style="font-size: 17px; color: rgb(134, 134, 134)"
                >Lorem ipsum dolor sit amet consectetur adipisicing elit. Dicta
                et dolorum voluptatum earum incidunt obcaecati eaque ut fugit,
                recusandae unde rem voluptate ipsum nemo ipsam qui, voluptates
                aliquam accusantium iure.</v-card-text
              >
              <v-card-actions class="mt-5 justify-center">
                <v-btn color="blue" variant="elevated" @click="resetData"
                  >Got it!</v-btn
                >
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-dialog>
  </div>
</template>
<script>
import { cartStroe } from "@/stores/cart";
import { mapActions } from "pinia";
export default {
  data: () => ({
    dialog: false,
  }),
  props: {
    popup: {
      type: Boolean,
    },
  },
  watch: {
    dialog(newVal) {
      if (!newVal) {
        this.$emit("close_popup");
      }
    },
  },
  methods: {
    ...mapActions(cartStroe, ["resetItem"]),
    resetData() {
      this.resetItem();
      this.dialog = false;
      this.$router.push({ name: "home" });
    },
  },
  mounted() {
    this.dialog = this.popup;
  },
};
</script>
