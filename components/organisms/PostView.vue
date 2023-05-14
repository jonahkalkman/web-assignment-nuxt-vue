<template>
  <div class="post-details">
    <SkeletonPostDetail v-if="loading" :loading="loading" />
    <!-- <Loading v-if="loading" /> -->

    <div v-else-if="!loading && post && validUrl" class="detail-wrapper">
      <img
        v-if="post.featuredMedia"
        :src="post.featuredMedia"
        class="detail-image"
      />
      <div v-if="post.title && post.content" class="detail-post mt-1-25">
        <h1 class="detail-title">{{ post.title }}</h1>
        <div class="detail-info">
          <span v-if="post.author" class="detail-author">
            {{ $t('post-detail.author-credit') }}
            {{ post.author }}
            {{ ' —' }}
          </span>
          <time v-if="post.date" class="detail-date"> {{ date() }}</time>
        </div>
        <div class="detail-content mt-1">
          <BaseText>
            {{ post.content }}
          </BaseText>
        </div>
      </div>
    </div>
    <div v-else class="detail-error">
      <Error />
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'nuxt-property-decorator'
import { Post } from '~/types/graphql/types'

@Component
export default class PostView extends Vue {
  @Prop({ required: true }) readonly post!: Post
  @Prop({ required: true }) readonly loading!: boolean
  @Prop({ required: true }) readonly validUrl!: boolean

  // TODO: Introduce util for date formatting
  date(): string {
    const date = new Date(this.post.date!)

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
.post-details {
  height: 100%;
}
.detail-wrapper {
  background-color: $white;
}
.detail-image {
  display: block;
  width: 100%;
}
.detail-post {
  padding-left: 16px;
  padding-right: 16px;
  padding-bottom: 20px;
}
.detail-title {
  font-family: $font-default;
  font-style: normal;
  font-weight: 600;
  font-size: 17px;
  line-height: 20px;
  color: $black;
  letter-spacing: -0.3px;
}
.detail-info {
  margin-top: 3px;
}
.detail-author {
  display: inline-block;
  font-family: $font-default;
  font-style: normal;
  font-weight: normal;
  font-size: 12px;
  line-height: 16px;
  color: $dark-grey;
}
.detail-date {
  display: inline-block;
  font-family: $font-default;
  font-style: normal;
  font-weight: normal;
  font-size: 12px;
  line-height: 16px;
  color: $dark-grey;

  letter-spacing: -0.2px;
}
.detail-content {
  overflow: hidden;
  width: 100%;
  font-family: $font-default;
  font-style: normal;
  font-weight: 400;
  font-size: 15px;
  line-height: 20px;
  color: $black;
  margin-top: 15px;
  letter-spacing: -0.2px;
}
.detail-error {
  padding-left: 16px;
  padding-right: 16px;
}
</style>
