# news-briefs

A Vue.js tutorial that uses TSX for its strongly typed templating support, and Vuetify for the goodness of Google Material. The baseline for the project is older but is derived from https://buttercms.com/blog/build-a-beautiful-animated-news-app-with-vuejs-and-vuetify?utm_campaign=Vue.js%20News&utm_medium=email&utm_source=Revue%20newsletter

For TSX and adaptations to work with Vue, see: https://scotch.io/tutorials/using-jsx-with-vue-and-why-you-should-care

For Vuetify with TSX support see: https://www.npmjs.com/package/vuetify-tsx

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev (notice: this runs on older < Vue 3.x CLI and therefore does not yet support starting web site with `npm run serve`)

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```
# production site available here: https://news-now.surge.sh
after running surge ./dist
$surge ./dist
    Running as calvin98115@yahoo.com (Student)
    project: ./dist
        domain: news-now.surge.sh
        upload: [====================] 100% eta: 0.0s (26 files, 5036586 bytes)
        CDN: [====================] 100%
        IP: 45.55.110.124
    Success! - Published to news-now.surge.sh


For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
