<script>
import 'prismjs'
import 'prismjs/themes/prism-tomorrow.css'
import 'prismjs/components/prism-bash'
import 'prismjs/components/prism-shell-session'
import 'prismjs/components/prism-json'
import 'prismjs/components/prism-python'
import 'prismjs/components/prism-yaml'
import 'prismjs/components/prism-graphql'
import 'prismjs/components/prism-javascript'

export default {
  async asyncData({ $notion, params, error }) {
    const pageTable = await $notion.getPageTable(
      "0edbc78b2aef4f1dab4f3eb6069dbb79"
    )
    const page = pageTable.find(
      (item) => item.public && item.slug === params.slug
    )
    const blockMap = await $notion.getPageBlocks(page ? page.id : params.slug)
    if (!blockMap || blockMap.error) {
      return error({ statusCode: 404, message: "Post not found" })
    }
    return { blockMap, page}
  },
  data() {
    return {
      pageLinkOptions: { component: "NuxtLink", href: "to" },
    }
  },
  head() {
    const post = this.page
    const title = post?.title
    const description = post?.description || "LearnerMetrics Support"
    const image = post?.thumbnail || null
    const tags = post.tags || title
    const href = `https://support.learnermetrics.com/posts/${post.slug}`
    const meta = this.$prepareMeta(
      {title, description, image, keywords: `${tags}`, url: href},
      [{name: "article:published-time", content: post?.created_at || null},]
    )
    return {
      title,
      link: [{rel: "canonical", href}],
      meta,
    }
  }
}
</script>


<template>
  <NotionRenderer :block-map="blockMap" :page-link-options="pageLinkOptions" full-page prism/>
</template>


<style>
@import "vue-notion/src/styles.css";
.notion-title, .notion-text, .notion-list, .notion-callout-text, p , h1, h2, h3, h4, span {
  @apply dark:text-white;
}
.notion-link{
  @apply dark:hover:bg-red-500;
}
</style>
