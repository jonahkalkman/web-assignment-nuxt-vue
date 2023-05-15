<template>
  <div class="navbar">
    <NuxtLink v-if="back" class="back" to="/">
      <img
        src="~/assets/images/icons/ic_chevron_right.svg"
        alt="back icon"
        height="12px"
        width="8px"
      />
    </NuxtLink>
    <NuxtLink to="/">
      <img v-if="faviconUrl" :src="faviconUrl" class="favicon" alt="logo" />
    </NuxtLink>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'nuxt-property-decorator'

@Component
export default class Navbar extends Vue {
  @Prop({ required: false, default: false }) readonly back!: boolean
  @Prop({ required: true }) readonly url!: string
  faviconData: any | null = null

  get faviconUrl(): string | null {
    if (!this.url) return null
    const { hostname } = new URL(this.url)
    if (!hostname) return null
    return 'https://api.faviconkit.com/' + hostname
  }

  goback() {
    return this.$router.back()
  }
}
</script>
<style lang="scss" scoped>
.navbar {
  height: 64px;
  width: 100%;
  position: relative;
  background-color: $white;
}
.back {
  position: absolute;
  left: 16px;
  top: 50%;
  transform: translateY(-50%);
  cursor: pointer;
}
.favicon {
  position: absolute;
  height: 24px;
  width: 24px;
  object-fit: contain;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
</style>
