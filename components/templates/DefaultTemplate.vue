<template>
  <div class="layout">
    <NavBar :url="url" :back="back" />
    <slot />
  </div>
</template>

<script lang="ts">
import { Vue, Component, Prop } from 'nuxt-property-decorator'

@Component
export default class DefaultTemplate extends Vue {
  @Prop({ required: true }) readonly url!: string
  @Prop({ required: false, default: false }) readonly back!: boolean
}
</script>

<style lang="scss" scoped>
.layout {
  height: 100%;
  background-color: $white;
}
</style>
