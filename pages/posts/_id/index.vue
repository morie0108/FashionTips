<template>
  <section class="container">
    <h1>{{ post.fields.title }}</h1>
    <v-row>
      <v-col>
        <div v-html="toHtmlString(post.fields.body)"></div>
      </v-col>
    </v-row>
  </section>
</template>

<script>
import { documentToHtmlString } from '@contentful/rich-text-html-renderer'
import { createClient } from '../../../plugins/contentful.js'

const client = createClient()

export default {
  async asyncData({ params, payload }) {
    // IDをキーに記事を取得
    if (payload)
      return {
        post: payload
      }
    const entry = await client.getEntry(params.id)
    return {
      post: entry
    }
  },
  methods: {
    toHtmlString(obj) {
      return documentToHtmlString(obj)
    }
  }
}
</script>
