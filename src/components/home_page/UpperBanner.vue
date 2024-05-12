<template>
  <div class="banner">
    <div class="parent">
      <img src="../../assets/images/banner-bg.jpg" />
      <div class="cont">
        <h3><span>Huge Saving</span> on UHD Televisions</h3>
        <p class="hint">Sale up to 70% off on selected items</p>
        <v-btn
          variant="outlined"
          style="border-radius: 30px; text-transform: none"
          density="compact"
          height="50"
          width="160"
          >Shop Now</v-btn
        >
      </div>
      <!-- <v-container>
        <v-row>
          <v-col cols="6">
            <div class="cont">
              <h3><span>Huge Saving</span> on UHD Televisions</h3>
              <p class="hint">Sale up to 70% off on selected items</p>
              <v-btn
                variant="outlined"
                style="border-radius: 30px; text-transform: none"
                density="compact"
                height="50"
                width="160"
                >Shop Now</v-btn
              >
            </div>
          </v-col>
        </v-row>
      </v-container> -->
    </div>
  </div>
</template>

<style lang="scss" scoped>
// .banner {
//   .parent {
//     height: 390px;
//     // background-image: url("../../assets/images/banner-bg.jpg");
//     background-size: cover;
//     background-position: -60 top;
//     .cont {
//       color: white;
//       padding: 40px 0 0 100px;
//       h3 {
//         font-size: 45px;
//         font-weight: 900;
//         span {
//           color: rgb(45, 251, 223);
//         }
//       }
//       .hint {
//         margin: 20px 0;
//       }
//     }
//   }
// }
.banner {
  position: relative;
  .parent {
    height: 390px;
    img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

    // background-image: url("../../assets/images/banner-bg.jpg");
    background-size: cover;
    background-position: -60 top;
    .cont {
      color: white;
      padding: 40px 0 0 100px;
      position: absolute;
      left: 40px;
      top: 20px;
      width: 600px;
      h3 {
        font-size: 45px;
        font-weight: 900;
        span {
          color: rgb(45, 251, 223);
        }
      }
      .hint {
        margin: 20px 0;
      }
    }
  }
}

// Media Query
@media (max-width: 990px) {
  .banner {
    .parent {
      height: 340px;
      .cont {
        padding-left: 20px;
        h3 {
          font-size: 30px;
        }
        width: 500px;
        left: 0;
      }
    }
  }
}
@media (max-width: 767px) {
  .banner {
    .parent {
      height: 320px;
      .cont {
        padding-left: 20px;
        h3 {
          white-space: pre-wrap;
          font-size: 20px;
        }
        width: 500px;
        left: 0;
      }
      .hint {
        font-size: 14px;
      }
    }
  }
}
@media (max-width: 580px) {
  .banner {
    .parent {
      height: 250px;
      .cont {
        padding-left: 20px;
        padding-top: 20px;
        h3 {
          white-space: pre-wrap;
          font-size: 15px;
        }
        width: 80%;
        left: 0;
      }
      .hint {
        font-size: 12px;
      }
      button {
        height: 30px !important;
        width: 130px !important;
        font-size: 11px !important;
      }
    }
  }
}
</style>
