<template>
  <!-- Use NuxtLink instead of 'open' method because Nuxt standard way to navigate  -->
  <!-- We lose some flexibility by choosing for NuxtLink instead of emitting on click because we cannot preform other things if a post is clicked -->
  <NuxtLink
    v-if="post.featuredMedia && post.title"
    :to="postUrl"
    class="first-post"
  >
    <img :src="post.featuredMedia" class="first-image" />
    <div class="first-title">{{ post.title }}</div>
  </NuxtLink>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'nuxt-property-decorator'
import { Post } from '~/types/graphql/types'

@Component
export default class FirstPost extends Vue {
  @Prop({ required: true }) readonly post!: Post

  // Use title in URL for SEO instead of only ID
  postUrl = `/${this.post?.title?.split(' ').join('-').toLowerCase()}?id=${
    this.post?.id
  }`
}
</script>
<style lang="scss" scoped>
.first-image {
  margin-left: 8px;
  margin-right: 8px;
  width: calc(100% - 16px);
  border-radius: 6px;
  object-fit: contain;
}
.first-post {
  position: relative;
  cursor: pointer;
}
.first-title {
  position: absolute;
  left: 16px;
  bottom: 8px;
  right: 16px;
  font-family: $font-default;
  font-style: normal;
  font-weight: 600;
  font-size: 12px;
  line-height: 17px;
  letter-spacing: -0.3px;
  color: $white;
  text-shadow: 0px 1px 1px rgba(0, 0, 0, 0.32);
}
</style>
