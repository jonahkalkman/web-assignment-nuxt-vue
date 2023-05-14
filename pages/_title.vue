<template>
  <DefaultTemplate :url="url" :back="true">
    <PostView
      :loading="$apollo.queries.post.loading"
      :post="post"
      :valid-url="urlValid"
    />
  </DefaultTemplate>
</template>

<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator'
import PostQuery from '@/graphql/queries/PostQuery.gql'
import { SITE_URL } from '@/constants/config'
import { Post, PostInput } from '~/types/graphql/types'

@Component({
  apollo: {
    post: {
      query: PostQuery,
      variables() {
        const post: PostInput = {
          id: this.id,
          url: this.url,
        }
        const variables = { post }
        return variables
      },
      result({ data }: any) {
        // Url title needs to match post title, otherwise show error
        this.urlValid =
          this.title === data.post?.title?.split(' ').join('-').toLowerCase()
      },
    },
  },
})
export default class Detail extends Vue {
  id: string | null = null
  title: string | null = null
  post: Post | null = null
  urlValid: boolean = true
  url = SITE_URL

  head() {
    return {
      title: this.post?.title,
    }
  }

  async asyncData({ route, params }: any) {
    const id = await route.query.id
    const title = await params.title

    return { id, title }
  }
}
</script>
