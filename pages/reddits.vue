<template>
  <div class="container">
    <input type="text"  v-model="input" /><button @click="searchReddit">search</button>
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
  data: function () {
    return { articles: [], input: '' }
  },
  transition: 'slide-right',
  async asyncData ({ query }) {
    const { data } = await axios.get('https://www.reddit.com/r/vue.json')
    return {
      articles: data.data.children
    }
  },
  methods: {
    searchReddit: function () {
      let self = this
      const word = this.input
      axios.get(`https://www.reddit.com/r/${word}.json`).then((response) => {
        self.articles = response.data.data.children
      }).catch((e) => {
        console.log(e)
      })
    }
  }
}
</script>
