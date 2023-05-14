<template>
  <div v-if="loading">
    <Skeleton class="skeleton-detail-image mb-20" width="100%" height="auto" />
    <div class="contained mb-1">
      <Skeleton class="mt-1-25" width="100%" height="60px" />
      <Skeleton class="mt-0-5" width="50%" height="18px" />
      <Skeleton class="mt-0-5" width="100%" height="200px" />
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'nuxt-property-decorator'

@Component
export default class SkeletonPostDetail extends Vue {
  @Prop({ required: true }) readonly loading!: boolean
}
</script>
<style lang="scss" scoped>
.skeleton-detail-image {
  aspect-ratio: 3 / 2;
}
</style>
