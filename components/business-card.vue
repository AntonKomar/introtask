<template>
  <v-card link height="100%">
    <img :src="business.preview_image || require('@/static/no-image.png')" />
    <v-chip link class="elevation-1 float-left chip-city white--text"
      ><span class="text-truncate">{{ city }}</span></v-chip
    >
    <business-logo :src="business.logo" :alt="business.title" />
    <v-btn
      class="mx-2 like-btn"
      fab
      color="white"
      @click="onLikeClick(business.id)"
    >
      <v-icon v-if="!business.is_liked" color="black" class="material-icons"
        >favorite_border</v-icon
      >
      <v-icon v-else-if="business.is_liked" color="black" class="material-icons"
        >favorite</v-icon
      >
    </v-btn>
    <div class="card-content pt-3 px-3">
      <div class="headline-sm text-truncate font-weight-bold">
        {{ business.title }}
      </div>
      <div v-if="business.tags" class="d-flex align-center">
        <v-chip link color="white" class="elevation-1 float-left"
          ><span class="text-truncate">{{ business.tags[1] }}</span></v-chip
        >
        <div
          v-if="business.tags && business.tags.length > 1"
          class="text-details tags-link ml-4"
        >
          +{{ business.tags.length - 1 }} weitere
        </div>
      </div>
      <div class="spacer"></div>
      <div class="mb-n1 pt-1">
        <div class="wrap text-body">{{ business.description }}</div>
      </div>
    </div>
  </v-card>
</template>

<script>
import BusinessLogo from './business-logo.vue'

export default {
  components: { BusinessLogo },
  props: {
    city: {
      type: String,
      default: '',
    },
    model: {
      type: Object,
      default() {
        return {}
      },
    },
  },
  watch: {
    model: {
      handler(val) {
        this.business = val
      },
      immediate: true,
    },
  },
  data() {
    return {
      business: this.model,
      businessCity: this.city,
    }
  },
  methods: {
    onLikeClick(id) {
      this.$store.commit('default/like', id)
    },
  },
}
</script>

<style lang="scss" scoped>
@import '@/assets/_breakpoints';
@import '@/assets/_vuetifycomponents';
@import '@/assets/_variables';

.v-card {
  position: relative;
}
.v-card img {
  width: 100%;
  height: 220px;
  object-fit: cover;
  @include md-and-up {
    height: 250px;
  }
}

.spacer {
  clear: both;
  margin-bottom: 10px;
}

.wrap {
  max-height: 100px;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.v-chip {
  margin: 0 !important;
  max-width: 110px;
}

.tags-link {
  color: $colorGrey2 !important;
}

.chip-city {
  position: absolute;
  right: 15px;
  top: 15px;
  background-color: $colorPrimaryBlack !important;
  border-color: $colorPrimaryBlack !important;
}

.like-btn {
  position: absolute;
  right: 15px;
  bottom: 206px;
  z-index: 99;
}

.like-btn .v-icon {
  font-size: 36px;
}
</style>
