<template>
  <section>
      <article v-for="(img, index) in media" :key="index" class="flipCard" :class=getId(index) :id=img.media_type>

        <div class="flipInner">       
          <div id="video" v-if="img.media_type === 'video' && img.url" class="flipFront">
            <iframe
              width="100%"
              height="250px"
              :src=img.url
              frameborder="0" 
              allowfullscreen>
            </iframe>
          </div>

          <div class="flipFront" v-if="img.media_type === 'image'">
            <img :src=img.url :alt=img.title>
          </div>

          <div class="flipBack">
            <a :href=img.hdurl>
              <h3>{{ img.title }}</h3>
            </a>
            <div v-if="img.explanation" class="explanation-container">
              <p>{{ img.explanation }}</p>
              <p v-if="img.copyright" class="copyright">Copyright: {{ img.copyright }}</p>
            </div> 
          </div>

        </div> 

      </article>
    </section>
</template>

<script>
export default {
  props: {
    media: {
      type: Array,
      required: true
    }
  }, 
  methods: {
   getId(index) {
     return 'pic' + index
   }
  }
}
</script>

<style scoped>
  section {
  padding: 0 30px 50px;
  min-height: 100vh;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
  grid-auto-rows: 250px;
  align-items: center;
  grid-column-gap: 5px;
  grid-row-gap: 5px;
  grid-auto-flow: dense;
}

#video {
  grid-column: span 1;
  grid-row: span 1;
}

article a {
  text-decoration: none;
  color: #FFF;
}

article img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

section > article:nth-child(3n) {
  grid-row: span 2;
}

section > article:nth-child(5n) {
  grid-row: span 3;
}

.flipCard {
  width: 100%;
  height: 100%;
  perspective: 1000px;
}  

.flipInner {
  background-color: rgb(15, 14, 27);
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.6s;
  transform-style: preserve-3d;
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
}

#image:hover .flipInner {
  transform: rotateY(180deg);
}

.flipFront, .flipBack {
  position: absolute;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
}

.flipBack {
  padding: 8px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  background-color: rgb(15, 14, 27);
  transform: rotateY(180deg);
}

.flipBack h3 {
  cursor: pointer;
  font-size: 18px;
  text-decoration: underline;
}

.explanation-container {
  overflow: hidden;
}

.explanation-container:hover {
  overflow-y: auto;
}

.copyright {
  margin-top: 5px;
  font-style: italic;
}
</style>