<template>
  <div class="wrapper">
    <div class="prevBread gt-xs" v-for="breadcrumb in prevElements">
      <router-link v-if="breadcrumb.route" :to="breadcrumb.route" class="no-hover">
        <q-btn class="text-white" flat small v-if="breadcrumb.name">{{ breadcrumb.name }}</q-btn>
      </router-link>
      <div class="label" v-if="!breadcrumb.route">
        <span v-if="breadcrumb.name">{{ breadcrumb.name }}</span>
      </div>
      <div> > </div>
    </div>
    <div v-if="lastElement">
      <div class="label lastElement" v-if="lastElement.name">{{ lastElement.name }}</div>
    </div>
  </div>
</template>

<script>
import { QBtn } from 'quasar'

export default {
  components: { QBtn },
  props: {
    breadcrumbs: { required: true },
  },
  computed: {
    prevElements () {
      return this.breadcrumbs.slice(0, this.breadcrumbs.length - 1)
    },
    lastElement () {
      return this.breadcrumbs[this.breadcrumbs.length - 1]
    },
  },
}
</script>

<style scoped lang="stylus">
@import '~variables'
.wrapper
  .prevBread, .q-btn, div
    display inline-block
  .label
    cursor auto
    text-overflow ellipsis
    justify-content center
    outline 0
    border
    vertical-align middle
    padding 0 16px
    font-weight 500
    text-transform uppercase
body.desktop .lastElement
    font-size 1.5rem
</style>
