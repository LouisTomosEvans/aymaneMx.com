<template>
  <div class="mt-20">
    <div class="flex justify-center items-center text-base font-semibold text-gray-600 dark:text-gray-300 mb-10">
      <h2 class="text-center">{{ title }}</h2>
    </div>

    <div class="wrapper-small flex flex-wrap my-5">
        <div v-for="post of posts" :key="post.slug" class="w-1/2 flex flex-wrap justify-center p-5">
        <nuxt-link :to="`/posts/${post.slug}`">
        <div class="h-80 flex bg-white dark:bg-gray-800 rounded-xl p-10 shadow-lg bg-background-form border">
          <div class="flex justify-center items-center content-center self-center align-center flex-wrap">
            <p class="w-full text-6xl text-center mb-6">{{ post.emoji }}</p>
            <h2 class="text-2xl w-full mb-3 text-center  font-bold text-gray-800 dark:text-gray-100">{{ post.title }}</h2>
            <p class="text-center text-lg text-gray-500 font-semibold dark:text-gray-400 my-1">{{ post.description }}</p>
          </div>
        </div>
        </nuxt-link>
      </div>
    </div>
  </div>
</template>


<script>
export default {
  props: {
    title: {
      type: String,
      default: "Our Documentation",
    },
    posts: {
      type: Array,
      default() {return []}
    },
  },
  methods: {
    formatDate(date) {
      const options = {year: 'numeric', month: 'long', day: 'numeric'}
      return new Date(date).toLocaleDateString('en', options)
    }
  },
}
</script>
