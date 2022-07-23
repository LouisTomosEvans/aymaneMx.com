<template>
  <Blogs :posts="posts" title="Our Documentation"/>
</template>


<script>
export default {
  async asyncData({$notion, params, error}) {
    const pageTable = await $notion.getPageTable("0edbc78b2aef4f1dab4f3eb6069dbb79")
    const posts = pageTable.filter((page) => page.public)
    return {posts}
  },
  head: {
    title: "AymaneMx's Blog",
    meta: [
      {
        hid: 'description',
        name: 'description',
        content: "aymaneMx's blog about python, django, vuejs."
      }
    ]
  }
}
</script>
