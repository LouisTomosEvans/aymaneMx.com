<template>
  <div class="wrapper-small md:px-10">
    <div class="h-96 mt-5">
      <Hero/>
    </div>

    <Blogs :posts="posts" title="Our Documentation" :critical="true"/>
    <!-- <Projects :projects="projects"/> -->
    <Contact class="pt-20" title="Can't find a solution? Get in touch!"/>
  </div>
</template>

<script>

export default {
  async asyncData({$notion, params, error}) {
    const pageTable = await $notion.getPageTable("0edbc78b2aef4f1dab4f3eb6069dbb79")
    const posts = pageTable.filter((page) => page.public)
    return {posts}
  },
}
</script>
