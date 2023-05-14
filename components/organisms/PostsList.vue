<template>
  <div class="wrapper">
    <SkeletonPostList v-if="loading" :loading="true" />
    <!-- <Loading v-if="loading" /> -->

    <div v-else-if="!loading && posts" class="posts">
      <BaseDivider />
      <FirstPost v-if="firstPost" :post="firstPost" class="mt-1" />
      <BaseDivider class="mt-1" />
      <template v-if="otherPosts">
        <OtherPost v-for="post in otherPosts" :key="post.id" :post="post" />
      </template>
    </div>
    <div v-else class="posts-error">
      <Error />
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'nuxt-property-decorator'
import { Post } from '~/types/graphql/types'

@Component
export default class PostsList extends Vue {
  @Prop({ required: true }) readonly posts!: Array<Post>
  @Prop({ required: true }) readonly loading!: boolean

  get firstPost(): Post | null {
    if (this.posts == null || this.posts.length === 0) {
      return null
    }
    return this.posts[0]
  }

  get otherPosts(): Array<Post> | null {
    return this.posts.slice(1)
  }
}
</script>
<style lang="scss" scoped>
.wrapper {
  background-color: $white;
  overflow-y: scroll;
  height: 100%;
}
.posts {
  height: 100%;
  width: 100%;
}
.posts-error {
  padding-left: 16px;
  padding-right: 16px;
}
</style>
