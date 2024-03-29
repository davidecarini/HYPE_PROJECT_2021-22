<!--
  Page: pois/Index
  Description: In this page are reported all the pois of the city represented in a carousel.
-->
<template>
  <main class="App">
    <!-- Header Section -->
    <TheHeader />

    <!-- BreadCrumb Section -->
    <section class="breadcrumb-section">
      <breadcrumb
        :default-route="[{ title: 'HOME', path: '/' }]"
        current-page="Punti di Interesse"
      />
    </section>

    <div class="carouselDiv">
      <div class="indicatorList">
        <div class="list">
          <carousel-indicator
            v-for="(poi, index) in poiList"
            :key="index"
            :index="index"
            :visibleSlide="visibleSlide"
            :title="poi.name"
            @change="change(index)"
          />
        </div>
      </div>
      <carousel @next="next" @prev="prev" class="carousel">
        <carousel-slide
          v-for="(poi, index) in poiList"
          :key="index"
          :index="index"
          :visibleSlide="visibleSlide"
          :id="poi.id"
          :name="'pois'"
          :direction="direction"
        >
          <div class="imageContainer" @wheel="wheel($event.deltaY)">
            <nuxt-link :to="`/pois/${poi.id}`">
              <img
                class="carouselImg"
                :src="require(`@/static/Poi/${poi.imgBackground}`)"
                :alt="poi.name"
              />
              <div class="textContainer-carousel">{{ poi.name }}</div>
              <div class="hoverText">{{ poi.carousel_desc }}</div>
            </nuxt-link>
          </div>
        </carousel-slide>
      </carousel>
      <div
        class="carouselScroll"
        v-for="(poi, index) in poiList"
        :key="index"
        :id="poi.id"
      >
        <div class="imageContainer container-scroll">
          <nuxt-link :to="`/pois/${poi.id}`">
            <img
              class="carouselImg image-scroll"
              :src="require(`@/static/Poi/${poi.imgBackground}`)"
              :alt="poi.name"
            />
            <div class="textContainer-scroll">{{ poi.name }}</div>
            <div class="hoverText scroll">{{ poi.carousel_desc }}</div>
          </nuxt-link>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import Carousel from '~/components/Carousel'
import CarouselSlide from '~/components/CarouselSlide'
import CarouselIndicator from '~/components/CarouselIndicator'
import TheHeader from '~/components/TheHeader'
import Breadcrumb from '~/components/Breadcrumb'

export default {
  layout: 'empty',

  data() {
    return {
      poiList: [],
      visibleSlide: 0,
      direction: 'left',
      loading: false,
      scrollingDirection: 0,
      lastScroll: 9999,
      scrollIdleTime: 2200, // time interval that we consider a new scroll event
    }
  },

  async asyncData({ $axios }) {
    const { data } = await $axios.get('api/pois')
    // const { data } = await $axios.get('http://localhost:3000/api/pois')
    return {
      poiList: data,
    }
  },

  computed: {
    slidesLen() {
      return this.poiList.length
    },
  },

  methods: {
    next() {
      if (this.visibleSlide >= this.slidesLen - 1) {
        this.visibleSlide = 0
      } else {
        this.visibleSlide++
      }
      this.direction = 'left'
      this.lastScroll = performance.now()
    },
    prev() {
      if (this.visibleSlide <= 0) {
        this.visibleSlide = this.slidesLen - 1
      } else {
        this.visibleSlide--
      }
      this.direction = 'right'
      this.lastScroll = performance.now()
    },
    change(index) {
      if (this.visibleSlide < index) {
        this.direction = 'left'
      } else {
        this.direction = 'right'
      }
      this.visibleSlide = index
    },
    wheel(deltaY) {
      //   if (deltaY > 0) {
      //     this.next()
      //   } else {
      //     this.prev()
      //   }
      // },
      const timeNow = performance.now()
      if (
        deltaY > 0 &&
        (this.scrollingDirection !== 1 ||
          timeNow > this.lastScroll + this.scrollIdleTime)
      ) {
        this.next()
        this.scrollingDirection = 1
      } else if (
        deltaY < 0 &&
        (this.scrollingDirection !== 2 ||
          timeNow > this.lastScroll + this.scrollIdleTime)
      ) {
        this.prev()
        this.scrollingDirection = 2
      }
      // this.lastScroll = performance.now()
    },

    goToDetails() {
      this.$router.push(`/details/${this.id}`)
    },
  },
  head() {
    return {
      title: 'insideBO • Punti di Interesse',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'This page groups some of the pois situated in the city',
        },
      ],
    }
  },
  components: {
    Carousel,
    CarouselSlide,
    TheHeader,
    CarouselIndicator,
    Breadcrumb,
  },
}
</script>

<style>
.breadcrumb-section {
  margin-top: 70px;
  background: transparent;
}
.carouselDiv {
  padding-top: 2%;
  padding-left: 4%;
  width: 100%;
  height: 90vh;
}
.imageContainer {
  position: relative;
  width: 70vw;
  height: 74vh;
  margin-top: 7vh;
  text-shadow: 0px 3px 3px rgba(0, 0, 0, 0.35);
  filter: brightness(90%);
}
.imageContainer:hover .hoverText,
.imageContainer.hover .hoverText {
  visibility: visible;
  opacity: 1;
  bottom: 5%;
  transition: 400ms ease-in-out;
  transition-delay: 200ms;
}
.imageContainer:hover .carouselImg,
.imageContainer.hover .carouselImg {
  -webkit-filter: blur(4px) brightness(70%);
  cursor: pointer;
  transition: 400ms ease-in-out;
  transition-delay: 200ms;
}
.imageContainer:hover .carouselImg.image-scroll,
.imageContainer.hover .carouselImg.image-scroll {
  -webkit-filter: blur(4px) brightness(70%);
  cursor: pointer;
  transition: 400ms ease-in-out;
  transition-delay: 200ms;
}
.imageContainer:hover .textContainer-carousel,
.imageContainer.hover .textContainer-carousel {
  bottom: 20%;
  transition: 400ms ease-in-out;
  transition-delay: 200ms;
}
.imageContainer:hover .textContainer-scroll,
.imageContainer.hover .textContainer-scroll {
  bottom: 20%;
  transition: 400ms ease-in-out;
  transition-delay: 200ms;
}
.carouselImg {
  display: block;
  margin-left: 0;
  width: 100%;
  height: 74vh;
  aspect-ratio: auto;
  object-fit: cover;
  transition: 400ms ease-in-out;
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
}
.carouselScroll {
  width: auto;
  left: 0;
  margin-right: 0;
}
.imageContainer.container-scroll {
  position: relative;
  height: 38vh;
  text-shadow: 0px 2px 2px rgba(0, 0, 0, 0.25);
  margin-left: 15vw;
  margin-right: 0;
}
img.carouselImg.image-scroll {
  display: block;
  margin-bottom: 50px;
  margin-left: 0;
  width: 70vw;
  height: 38vh;
  aspect-ratio: auto;
  object-fit: cover;
}
div.textContainer-scroll {
  color: white;
  font-size: 5vw;
  line-height: normal;
  font-family: 'Josefin Sans';
  text-transform: uppercase;
  float: left;
  position: absolute;
  width: 56%;
  margin-bottom: 0;
  bottom: 0;
  transition: 400ms ease-in-out;
}
div.textContainer-carousel {
  color: white;
  font-size: 5vw;
  line-height: normal;
  font-family: 'Josefin Sans';
  text-transform: uppercase;
  float: left;
  position: absolute;
  width: 56%;
  margin-bottom: 0;
  bottom: 0;
  transition: 400ms ease-in-out;
}
div.hoverText {
  color: white;
  font-size: 2vw;
  line-height: normal;
  font-family: 'Josefin Sans';
  font-style: italic;
  float: left;
  position: absolute;
  margin-bottom: 0;
  bottom: 0;
  height: auto;
  left: 5px;
  visibility: hidden;
  opacity: 0;
  transition: 400ms ease-in-out;
  width: 70vw;
}
div.hoverText.scroll {
  width: 70vw;
}
span {
  top: 50%;
  /*border: solid 2px yellow;*/
}
.App {
  background-color: #f2f2f2;
  height: auto;
}
body {
  overscroll-behavior-y: none;
  background-color: #f2f2f2;
}
div.indicatorList {
  /*border: solid 2px blue;*/
  width: 20vw;
  height: 76vh;
  position: relative;
  float: right;
  margin-top: 4%;
  margin-right: 2%;
  padding: 0;
  font-size: 20px;
}
/* Mobile visualization without indicator list*/
@media screen and (max-width: 880px) {
  .indicatorList {
    display: none;
  }
  .carousel {
    display: none !important;
  }

  .carouselDiv {
    padding-left: 0;
  }
}

/* Desktop visualization */
@media screen and (min-width: 881px) {
  .carouselScroll {
    display: none;
  }
}
</style>
