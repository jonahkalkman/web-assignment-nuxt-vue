<template>
  <div v-if="loading" class="container mt-1">
    <Skeleton class="mb-20 skeleton-featured" width="100%" height="auto" />
    <div class="skeleton-post mt-2">
      <Skeleton width="96px" height="64px" />
      <div class="skeleton-content">
        <Skeleton class="mb-0-5" width="100%" height="28px" />
        <Skeleton width="50%" height="14px" />
      </div>
    </div>
    <div class="skeleton-post mt-2">
      <Skeleton width="96px" height="64px" />
      <div class="skeleton-content">
        <Skeleton class="mb-0-5" width="100%" height="28px" />
        <Skeleton width="50%" height="14px" />
      </div>
    </div>
    <div class="skeleton-post mt-2">
      <Skeleton width="96px" height="64px" />
      <div class="skeleton-content">
        <Skeleton class="mb-0-5" width="100%" height="28px" />
        <Skeleton width="50%" height="14px" />
      </div>
    </div>
    <div class="skeleton-post mt-2">
      <Skeleton width="96px" height="64px" />
      <div class="skeleton-content">
        <Skeleton class="mb-0-5" width="100%" height="28px" />
        <Skeleton width="50%" height="14px" />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'nuxt-property-decorator'

@Component
export default class SkeletonPostList extends Vue {
  @Prop({ required: true }) readonly loading!: boolean
}
</script>
<style lang="scss" scoped>
.skeleton-featured {
  aspect-ratio: 3 / 2;
}
.skeleton-post {
  display: flex;
  gap: 8px;
}
.skeleton-content {
  display: flex;
  flex-direction: column;
  flex: auto;
}
</style>
