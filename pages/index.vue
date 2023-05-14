<template>
  <DefaultTemplate :url="url">
    <PostsList :posts="posts" :loading="$apollo.queries.posts.loading" />
  </DefaultTemplate>
</template>

<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator'
import PostsQuery from '@/graphql/queries/PostsQuery.gql'
import { SITE_TITLE, SITE_URL } from '@/constants/config'
import { ListPostsInput, Post } from '~/types/graphql/types'

@Component({
  apollo: {
    posts: {
      query: PostsQuery,
      variables() {
        const posts: ListPostsInput = {
          url: this.url,
        }
        const variables = { posts }
        return variables
      },
    },
  },
})
export default class Index extends Vue {
  posts: Array<Post> | null = null
  url = SITE_URL

  head() {
    return {
      title: SITE_TITLE,
    }
  }
}
</script>
