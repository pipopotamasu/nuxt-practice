<template>
  <div class="container">
    <ul>
      <li v-for="article in articles" :key="article.data.id">
        <a :href="article.data.url">
          <span>{{ article.data.title }}</span>
        </a>
      </li>
    </ul>
    <p><nuxt-link to="/">Back home</nuxt-link></p>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  transition: 'slide-right',
  async asyncData ({ query }) {
    const { data } = await axios.get('https://www.reddit.com/r/vue.json')
    return {
      articles: data.data.children
    }
  }
}
</script>
