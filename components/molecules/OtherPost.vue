<template>
  <!-- Used NuxtLink instead of 'open' method because Nuxt standard way to navigate  -->
  <!-- We lose some flexibility by choosing for NuxtLink instead of emitting on click because we cannot preform other things if a post is clicked -->
  <NuxtLink v-if="post.featuredMedia && post.title" :to="postUrl">
    <div class="other-post">
      <img :src="post.featuredMedia" class="other-image" :alt="post.title" />
      <div class="other-post-content">
        <div class="other-title">{{ post.title }}</div>
        <div class="other-date">{{ date() }}</div>
      </div>
    </div>
    <BaseDivider />
  </NuxtLink>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'nuxt-property-decorator'
import { Post } from '~/types/graphql/types'

@Component
export default class OtherPost extends Vue {
  @Prop({ required: true }) readonly post!: Post

  // Use title in URL for SEO instead of only ID
  postUrl = `/${this.post?.title?.split(' ').join('-').toLowerCase()}?id=${
    this.post?.id
  }`

  date(): string {
    if (!this.post.date) return ''
    const date = new Date(this.post.date)

    const options: Intl.DateTimeFormatOptions = {
      year: 'numeric',
      month: 'short',
      day: 'numeric',
    }
    return date.toLocaleDateString(this.$i18n.locale, options)
  }
}
</script>
<style lang="scss" scoped>
.other-post {
  display: flex;
  width: 100%;
  padding-top: 12px;
  padding-bottom: 12px;
  cursor: pointer;
}
.other-image {
  margin-left: 8px;
  margin-right: 8px;
  width: 96px;
  border-radius: 4px;
  object-fit: contain;
}
.other-title {
  font-family: $font-default;
  font-style: normal;
  font-weight: 500;
  font-size: 10px;
  line-height: 14px;
  letter-spacing: -0.2px;
  color: $black;
}
.other-date {
  font-family: $font-default;
  font-style: normal;
  font-weight: normal;
  font-size: 10px;
  line-height: 14px;
  letter-spacing: -0.2px;
  color: $date-grey;
}
</style>
