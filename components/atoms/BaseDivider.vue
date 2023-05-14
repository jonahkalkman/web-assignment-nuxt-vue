<template>
  <div class="divider"><slot /></div>
</template>

<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator'

@Component
export default class BaseDivider extends Vue {}
</script>

<style lang="scss" scoped>
.divider {
  background-color: $light-grey;
  height: 1px;
  width: 100%;
}
</style>
