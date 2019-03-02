<template>
    <v-app dark>
        <!--Top Menu Navigation -->
        <v-toolbar fixed app light clipped-left color="black" class="elevation-2">
            <v-toolbar-side-icon @click="toggleSideBar" class="white--text"></v-toolbar-side-icon>
            <v-toolbar-title class="white--text">News App</v-toolbar-title>
        </v-toolbar>
        <!--The SideBar menu component go here -->
        <SideBar v-bind:NewsAPIKey='NewsAPIKey' 
            v-bind:drawer='drawer' 
            v-on:blur='toggleSideBar'
            v-on:selectSource='setNewsChannel'/>
        <!--Main Content -->
        <v-content>
            <v-container fluid>
                <!--The Main Content component go here-->
                <NewsArticles :articles='articles' />
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
    import SideBar from '@/components/SideBar'
    import NewsArticles from '@/components/NewsArticles.vue'
    // const NewsAPIKey = 'b8f2d3ccc2de4b108a18205b2ae9d2c6'
  
    export default {
        components: {
            NewsArticles,
            SideBar
          },
        data() {
            return {
                NewsAPIKey:  'b8f2d3ccc2de4b108a18205b2ae9d2c6', 
                drawer: true,
                articles: [],
                errors: []
            };
        },
        async created() {
            const requestUrl = `https://newsapi.org/v2/top-headlines?sources=techcrunch&apiKey=${this.NewsAPIKey}`
            console.log(`RequestUrl: ${requestUrl}`)
            await Axios.get(requestUrl)
                .then(response => {
                    console.log(`Response of articles: ${response.data.articles}`)
                    this.articles = response.data.articles
                }).catch(error => this.errors.push(error))
        },
        methods: {
          toggleSideBar(){
              this.drawer = !this.drawer
              console.log(`toggled drawer to: ${this.drawer}`)
          },
          setNewsChannel(channelId) {
              const requestUrl = `https://newsapi.org/v2/top-headlines?sources=${channelId}&apiKey=${this.NewsAPIKey}`
              console.log(`App::setNewsChannel - RequestUrl: ${requestUrl}`)
              Axios.get(requestUrl)
                .then(response => this.articles = response.data.articles)
                .catch(error => {
                  console.log(`Fetch News for channel error: ${error}`)
                  this.errors.push(error)
                })
            }
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
