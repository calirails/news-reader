<template>
  <v-app light>
    <!--The Side Menu component go here -->
    <v-toolbar fixed app light clipped-left color="primary" class="elevation-2">
      <v-toolbar-side-icon @click="drawer = !drawer" class="white--text"></v-toolbar-side-icon>
      <v-toolbar-title class="white--text">News App</v-toolbar-title>
    </v-toolbar>
    <v-content>
      <v-container fluid>
        <!--The Main Content component go here-->
        <NewsArticles v-bind:articles='this.articles' />
      </v-container>
    </v-content>
    <v-footer class="secondary" app>
      <v-layout row wrap align-center>
        <v-flex xs12>
          <div class="white--text ml-3">
            Made with
            <v-icon class="red--text">favorite</v-icon>by
            <a class="white--text" href="https://vuetifyjs.com" target="_blank">Vuetify</a>
            and
            <a
              class="white--text"
              href="https://github.com/rachidsakara"
              target="_blank"
            >Rachid Sakara</a>
          </div>
        </v-flex>
      </v-layout>
    </v-footer>
  </v-app>
</template>
<script>
  import Axios from 'axios'
  import NewsArticles from '@/components/NewsArticles.vue'
  const NewsAPIKey = 'b8f2d3ccc2de4b108a18205b2ae9d2c6'
  
  export default {
    components: {
      NewsArticles
    },
    data() {
      return {
        drawer: true,
        articles: [],
        errors: []
      };
    },
    async created() {
      const requestUrl = `https://newsapi.org/v2/top-headlines?sources=techcrunch&apiKey=${NewsAPIKey}`
      console.log(`RequestUrl: ${requestUrl}`)
      await Axios.get(requestUrl)
        .then(response => {
          console.log(`Response of articles: ${response.data.articles}`)
          this.articles = response.data.articles
        }).catch(error => this.errors.push(error))
    }
  };
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
