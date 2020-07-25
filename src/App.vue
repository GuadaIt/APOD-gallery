<template>
  <div id="app">
    <Header />
    <Loading v-if="isLoading && !error"/>
    <Error v-show="error"/>
    <Gallery else :media="media"/>
  </div>
</template>

<script>
import Loading from "./components/Loading.vue";
import Header from "./components/Header.vue";
import Gallery from "./components/Gallery.vue";
import Error from "./components/Error.vue";

export default {
  name: "App",
  components: {
    Loading,
    Error,
    Header,
    Gallery
  },
  data() {
    return {
      media: [],
      isLoading: true,
      error: null
    };
  },
  mounted() {
    fetch(`https://api.nasa.gov/planetary/apod?api_key=${process.env.VUE_APP_API_KEY}&count=50`)
      .then(res => {
        if(!res.ok) {
          throw Error(res.statusText)
        }
        return res.json()
      })
      .then(dataJson => {
        let data = dataJson;
        data.forEach((media) => {
          if (media.url.search(/http/i) === -1) {
            media.url = "https:" + media.url;
          }
          if (media.explanation.indexOf("digg") != -1) {
            media.explanation = media.explanation.substring(0, media.explanation.indexOf("digg"));
          }
        });
        this.media.push(...data);
        this.isLoading = false;
      })
      .catch(error => this.error = error)
  }
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: monospace;
}

body {
  min-height: 100vh;
  color: white;
  background-image: url("./assets/starfield-banner.jpg");
  background-repeat: repeat;
  background-size: contain;
}

::-webkit-scrollbar {
  width: 10px;
}

::-webkit-scrollbar-track {
  background-color: rgb(15, 14, 27);
  border: 1px solid #000;
}

::-webkit-scrollbar-thumb {
  border-radius: 5px;
  background-color: #fff;
}

::-webkit-scrollbar-thumb:hover {
  background-color: #fff;
}

#app {
  min-height: 100vh;
  text-align: center;
}
</style>
