<template>
  <div class="skeleton" :style="{ width: width, height: height }"></div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'nuxt-property-decorator'

@Component
export default class Loading extends Vue {
  @Prop({ required: true }) readonly width!: string
  @Prop({ required: true }) readonly height!: string
}
</script>

<style lang="scss" scoped>
.skeleton {
  display: block;
  width: 100%;
  height: 100%;
  border-radius: 0.25rem;
  animation: loading 1s linear infinite alternate;
}
@keyframes loading {
  0% {
    background-color: hsl(200, 20%, 80%);
  }
  100% {
    background-color: hsl(200, 20%, 95%);
  }
}
</style>
