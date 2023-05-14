<template>
  <p class="error">{{ $t('post-detail.error') }}</p>
</template>

<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator'

@Component
export default class BaseText extends Vue {}
</script>

<style lang="scss" scoped>
.error {
  color: $error;
  font-family: Inter;
  font-size: 17px;
  line-height: 20px;
}
</style>
