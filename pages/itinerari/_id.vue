<!--
  Page: Itinerari/_id
  Description: In this page is described a specific itinerary.
-->
<template>
  <main class="page-container">
    <div class="body-container">
      <StaticHalfImage
        :slide="`../Itineraries/${imgBackground}`"
        :title="Itname"
      />
      <section class="breadcrumb-section5">
        <breadcrumb
          :default-route="[
            { title: 'HOME', path: '/' },
            { title: 'Itinerari', path: '/Itinerari/' },
          ]"
          :current-page="Itname"
        />
      </section>

      <div class="title-container">I LUOGHI DELL'ITINERARIO</div>

      <ItineraryPath
        line="/Itineraries/LineaDrittaPNG.png"
        :name1="namePoi1"
        :name2="namePoi2"
        :name3="namePoi3"
        :name4="namePoi4"
        :name5="namePoi5"
        :id1="idPoi1"
        :id2="idPoi2"
        :id3="idPoi3"
        :id4="idPoi4"
        :id5="idPoi5"
        :img1="img1"
        :img2="img2"
        :img3="img3"
        :img4="img4"
        :img5="img5"
      />

      <section class="section-description">
        <div class="title-container">DESCRIZIONE</div>
        <p class="text-container">{{ description }}</p>
      </section>
      <section class="section-description">
        <div class="title-container">DURATA</div>
        <p class="text-container">{{ duration }}</p>
      </section>

      <section class="section-description">
        <div class="title-container">MAPPA ITINERARIO</div>
        <div class="map-container">
          <a target="_blank" :href="link">
            <img
              class="map-image"
              :src="require(`@/static/Itineraries/${this.map}`)"
            />
          </a>
          <div class="map-text">
            <a
              target="_blank"
              style="text-decoration: none; color: #c13939"
              :href="link"
              >Apri in Maps</a
            >
          </div>
        </div>
      </section>

      <div class="button-container">
        <baseButton title="Tutti gli itinerari" goto="/itinerari/" />
      </div>
    </div>
  </main>
</template>

<script>
import CommonMixin from '~/mixins/common'
import staticHalfImage from '~/components/StaticHalfImage'
import Breadcrumb from '~/components/Breadcrumb.vue'
// import cardInfo from '~/components/CardInfo'
import ItineraryPath from '~/components/ItineraryPath'

export default {
  name: 'DetailsPage',
  mixins: [CommonMixin],
  components: {
    staticHalfImage,
    Breadcrumb,
    // cardInfo,
    ItineraryPath,
  },

  async asyncData({ route, $axios }) {
    const { id } = route.params
    const [data1, data2] = await Promise.all([
      // $axios.get('http://localhost:3000/api/itineraries/' + id),
      // $axios.get('http://localhost:3000/api/itPoi/' +id),
      $axios.get('api/itineraries/' + id),
      $axios.get('api/itPoi/' + id),
    ])

    return {
      Itname: data1.data[0].name,
      duration: data1.data[0].duration,
      imgBackground: data1.data[0].imgBackground,
      description: data1.data[0].description,
      map: data1.data[0].map,
      link: data1.data[0].link,
      namePoi1: data2.data[0].pois[0].name,
      namePoi2: data2.data[0].pois[1].name,
      namePoi3: data2.data[0].pois[2].name,
      namePoi4: data2.data[0].pois[3].name,
      namePoi5: data2.data[0].pois[4].name,
      idPoi1: data2.data[0].pois[0].id,
      idPoi2: data2.data[0].pois[1].id,
      idPoi3: data2.data[0].pois[2].id,
      idPoi4: data2.data[0].pois[3].id,
      idPoi5: data2.data[0].pois[4].id,
      img1: data2.data[0].pois[0].imgBackground,
      img2: data2.data[0].pois[1].imgBackground,
      img3: data2.data[0].pois[2].imgBackground,
      img4: data2.data[0].pois[3].imgBackground,
      img5: data2.data[0].pois[4].imgBackground,
    }
  },

  methods: {
    backToList() {
      this.$router.push('/itinerari/')
    },
  },
  head() {
    return {
      title: 'insideBO • ' + this.Itname,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'This page describes a particular itinerary',
        },
      ],
    }
  },
  mounted() {
    const date = new Date()
    // Example on hwo to use mixinx
    console.log(this.formatMyDate(date.toLocaleDateString()))
  },
}
</script>
<style>
.section-description {
  font-family: 'Raleway', 'Avenir', sans-serif;
  font-style: normal;
  margin-left: 8px;
  margin-right: 8px;
  background-color: #f2f2f2;
  text-align: justify;
  text-justify: inter-word;
}

.page-container {
  margin-top: -65px;
  background-color: #f2f2f2;
}
.body-container {
  margin-top: 110px;
}

.title-container {
  margin-top: 50px;
  width: 100%;
  font-family: 'Josefin Sans';
  font-style: normal;
  font-weight: 600;
  font-size: 30px;
  line-height: 50px;
  color: #c13939;
  background-color: #f2f2f2;
  padding-left: 80px;
}
.row {
  margin: auto;
  width: 100%;
  justify-content: center;
  padding: 10px;
}
.button-container {
  width: 100%;
  height: 100px;
  padding: 20px;
}

.text-container {
  padding-top: 10px;
  padding-left: 8vw;
  padding-right: 8vw;
  font-size: 22px;
}

.button-container {
  text-align: right;
}

.breadcrumb-section5 {
  margin-right: 20px;
  margin-top: -5px;
}
.main-page {
  background-color: #f2f2f2;
}

.map-container {
  margin: 20px;
  width: 60%;
  overflow: hidden;
  transition: 300ms ease-in-out;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-left: auto;
  margin-right: auto;
  border-radius: 10px;
  border: 5px solid #c13939;
}

.map-image {
  aspect-ratio: auto;
  object-fit: cover;
  width: 100%;
  height: 100%;
  transition: 300ms ease-in-out;
  text-align: center;
}

.map-container:hover .map-text,
.map-container.hover .map-text {
  opacity: 1;
  transition: 300ms ease-in-out;
}

.map-container:hover .map-image,
.map-container.hover .map-image {
  opacity: 0.3;
  transition: 300ms ease-in-out;
}
.map-text {
  opacity: 0;
  color: #c13939;
  position: absolute;
  text-align: center;
  text-justify: inter-word;
  font-family: 'Josefin Sans';
  text-transform: uppercase;
  font-size: 2vw;
}

@media screen and (max-width: 500px) {
  .title-container {
    padding-left: 0px;
    text-align: center;
  }
  .map-container {
    border: none;
    border-radius: 0;
  }
  .text-container {
    font-size: 16px;
  }
}
@media screen and (max-width: 1000px) {
  .map-container {
    width: 100%;
  }
}
</style>
