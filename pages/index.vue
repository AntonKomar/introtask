<template>
  <div class="container">
    <business-list
      :businesses="businesses"
      :type="type"
      :city="city"
      :allBusinessesQuontity="allBusinessesQuontity"
    />
  </div>
</template>

<script>
import BusinessList from '../components/business-list.vue'

export default {
  components: { BusinessList },
  data() {
    return {
      type: 'Arbeitgeber',
      city: 'Passau',
      businesses: [],
      allBusinessesQuontity: 0,
    }
  },
  mounted() {
    this.allBusinessesQuontity = this.$store.getters[
      'default/getBusinessesLength'
    ]
    this.businesses = this.$store.getters['default/getFixedNumberOfBusinesses'](
      5
    )
  },
}
</script>

<style lang="scss" scoped>
@import '@/assets/_breakpoints';

.container {
  padding: 0 24px;
  @include md-and-up {
    padding: 0 80px;
  }
}
</style>
