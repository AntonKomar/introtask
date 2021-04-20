<template>
  <div v-if="businesses.length" class="my-3">
    <h2 class="headline-lg">
      Einzigartige <strong>{{ type }}</strong> aus
      <strong>{{ city }}</strong>
    </h2>
    <div v-swiper="swiperOption" class="overflow-visible relative">
      <div class="swiper-wrapper">
        <div
          :key="business.id"
          v-for="(business, i) in businesses"
          class="swiper-slide lg"
        >
          <business-card :model="businesses[i]" :city="city" />
        </div>
        <span
          v-if="showMoreBusinesses > 0"
          slot="container-end"
          class="swiper-slide"
        >
          <v-card link height="100%" class="end-slide">
            <div class="background-image"></div>
            <div
              class="content text-center d-flex flex-column justify-space-between align-center"
            >
              <div class="mt-5">
                <div class="headline-sm mb-0 white--text">
                  Entdecke über
                  {{ showMoreBusinesses }} weitere<br />
                </div>
                <div class="headline-md mb-0 white--text">
                  <strong>Unternehmen</strong>
                </div>
              </div>
              <v-btn primary rounded x-large class="mb-5 btn-primary">
                Alle anzeigen
              </v-btn>
            </div>
          </v-card>
        </span>
      </div>
      <div class="swiper-button-container">
        <v-btn icon class="mx-2 swiper-button-next">
          <v-icon small color="black" class="material-icons"
            >arrow_forward_ios</v-icon
          >
        </v-btn>
        <v-btn icon class="mx-2 swiper-button-prev">
          <v-icon small color="black" class="material-icons"
            >arrow_back_ios</v-icon
          >
        </v-btn>
      </div>
    </div>
  </div>
</template>

<script>
import { directive } from 'vue-awesome-swiper'
import BusinessCard from './business-card.vue'

export default {
  components: { BusinessCard },
  directives: {
    swiper: directive,
  },
  props: {
    type: {
      type: String,
      default: '',
    },
    city: {
      type: String,
      default: '',
    },
    businesses: {
      type: Array,
      default() {
        return []
      },
    },
    allBusinessesQuontity: {
      type: Number,
      default: 0,
    },
  },
  data() {
    return {
      businessesQuontity: this.allBusinessesQuontity,
      businessesArray: this.businesses,
      swiperOption: {
        spaceBetween: 30,
        slidesPerView: 'auto',
        navigation: {
          nextEl: '.swiper-button-next',
          prevEl: '.swiper-button-prev',
        },
        breakpoints: {
          768: {
            slidesPerView: 'auto',
          },
          640: {
            slidesPerView: 2,
          },
          320: {
            slidesPerView: 1,
          },
        },
      },
    }
  },
  watch: {
    allBusinessesQuontity: {
      handler(val) {
        this.businessesQuontity = this.allBusinessesQuontity
      },
      immediate: true,
    },
    businesses: {
      handler(val) {
        this.businessesArray = this.businesses
      },
      immediate: true,
    },
  },
  computed: {
    showMoreBusinesses() {
      return this.businessesQuontity - this.businessesArray.length
    },
  },
}
</script>
<style lang="scss" scoped>
@import '@/assets/_variables';
@import '@/assets/_breakpoints';
@import '@/assets/_vuetifycomponents';
@import '@/assets/_shadows';

.relative {
  position: relative;
}

.overflow-visible {
  overflow: visible;
}

.swiper-slide {
  height: auto;
  align-self: stretch;
}

.swiper-slide {
  width: 330px !important;
  &.lg {
    @include md-and-up {
      width: 510px !important;
    }
  }
}

.end-slide {
  position: relative;
  overflow: hidden;
}

.background-image {
  display: block;
  background-image: url('https://miro.medium.com/max/1020/1*qH3ffeXGMZY9SBtjCxdb5g.jpeg');
  height: 100%;
  -webkit-filter: blur(15px);
  -moz-filter: blur(15px);
  -o-filter: blur(15px);
  -ms-filter: blur(15px);
  filter: blur(15px);
}

.content {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.btn-primary {
  background: $gradientPrimary !important;
  color: $colorPrimaryWhite !important;
  font-weight: 700 !important;
  font-size: 22px !important;
  box-shadow: 0 3px 15px 0 rgba(11, 161, 219, 0.25) !important;
}

.swiper-button-container {
  display: none;
  justify-content: space-between;
  width: 100px;
  height: 36px;
  position: absolute;
  top: -50px;
  right: 100px;
  @include md-and-up {
    display: flex;
  }
}
.swiper-button-prev {
  width: 20px;
  height: 36px;
}
.swiper-button-next {
  width: 20px;
  height: 36px;
}

.swiper-button-next:focus {
  outline: none;
  box-shadow: none;
}

.swiper-button-container i {
  font-size: 24px !important;
}

.swiper-button-next:after,
.swiper-container-rtl .swiper-button-prev:after {
  content: unset !important;
}
.swiper-button-prev:after,
.swiper-container-rtl .swiper-button-next:after {
  content: unset !important;
}
</style>
