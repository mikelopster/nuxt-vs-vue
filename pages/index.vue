<script setup>
import blogs from '~/data/blogs.json'
import { ref } from 'vue'

const firstname = ref('')

useHead({
  title: 'Mikelopster App',
  meta: [
    { name: 'description', content: 'My amazing site.' }
  ],
  bodyAttrs: {
    class: 'test'
  },
  script: [ { innerHTML: 'console.log(\'Hello world\')' } ]
})
</script>

<template>
  <div>
    <div>
      Firstname {{ firstname }}
      <input v-model="firstname">
    </div>
    <h1>Blog List</h1>
    <ul>
      <li v-for="blog in blogs" :key="blog.id">
        <nuxt-link :to="`/blog/${blog.id}`">{{ blog.title }}</nuxt-link>
      </li>
    </ul>
  </div>
</template>

