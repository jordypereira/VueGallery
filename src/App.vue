<template>
  <div id="app">
    <div class="container">
      <ul class="filters">
        <li v-for="filter in filters" :key="filter.tag" @click="changeFilter(filter.tag)">{{ filter.name }}</li>
      </ul>
      <div class="grid">
        <project v-for="(project, i) in filteredProjects" :key="i" :items="project" :class="project.size" v-on:showSlideshow="showSlideshow" />
      </div>
    </div>
    <slideshow v-if="slideshow" :images="images" v-on:hideSlideshow="hideSlideshow" />
  </div>
</template>

<script>
import Project from './components/Project';
import Slideshow from './components/Slideshow';
import tuinJensVoor from './assets/projects/tuin_jens_voor.jpg';
import tuinJensTijdens1 from './assets/projects/tuin_jens_tijdens1.jpg';
import tuinJensTijdens2 from './assets/projects/tuin_jens_tijdens2.jpg';
import tuinJensNa from './assets/projects/tuin_jens_na.jpg';
import marioOprit from './assets/projects/carwrapping_marioKart_oprit.jpg';
import marioBr from './assets/projects/carwrapping_marioKart_br.jpg';
import yvesTuinNa from './assets/projects/tuinaanleg_yves_tuin_na_2.jpg';
import tuinDegerVoor from './assets/projects/tuin_deger_voor.jpg';
import tuinDegerTijdens1 from './assets/projects/tuin_deger_tijdens1.jpg';
import tuinDegerTijdens2 from './assets/projects/tuin_deger_tijdens2.jpg';
import tuinDegerNa from './assets/projects/tuin_deger_na.jpg';

export default {
  name: 'app',
  components: {
    Project,
    Slideshow,
  },
  methods: {
    changeFilter: function(tag) {
      this.filter = tag;
    },
    showSlideshow(images) {
      this.images = images;
      this.slideshow = true;
    },
    hideSlideshow() {
      this.slideshow = false;
      this.images = [];
    },
  },
  computed: {
    filteredProjects: function() {
      if (!this.filter) {
        return this.projects;
      }
      return this.projects.filter(project => project.tag == this.filter);
    },
  },
  data() {
    return {
      slideshow: false,
      filter: null,
      filters: [
        {
          name: 'All Works',
          tag: null,
        },
        {
          name: 'Carwrapping',
          tag: 'carwrapping',
        },
        {
          name: 'Tuinonderhoud en aanleg',
          tag: 'tuin',
        },
        {
          name: 'Schilderen',
          tag: 'schilderen',
        },
        {
          name: 'Webdesign',
          tag: 'web',
        },
      ],
      images: [],
      projects: [
        {
          featured: { img: tuinJensNa, description: 'Jens Tuin aanleg' },
          title: 'Tuinaanleg JP',
          description: 'Aanleg rolgazon 80m².',
          tag: 'tuin',
          size: ['item--wide', 'item--large'],
          images: [
            { img: tuinJensVoor, description: 'Jens Tuin aanleg' },
            {
              img: tuinJensTijdens1,
              description:
                'Plaatsen van afsluiting, boordstenen, poortjes. Planten van bomen, aanleg gazon. Instaleren waterdichte verlichting in de steentjes.',
            },
            { img: tuinJensTijdens2, description: 'Jens Tuin aanleg' },
          ],
        },
        {
          featured: { img: marioOprit, description: 'Mario Oprit aanleg' },
          title: 'Carwrapping JP',
          description:
            'Mario kart met kleuren: Perfect Satin Blue en Satin Smoldering Red en Satin black gold dust..',
          tag: 'carwrapping',
          size: 'item--large',
          images: [{ img: marioBr, description: 'Mario Tuin aanleg' }],
        },
        {
          featured: { img: yvesTuinNa, description: 'Yves Tuin aanleg' },
          title: 'Tuinaanleg JP',
          description:
            'Plaatsen van afsluiting, boordstenen, poortjes. Planten van bomen, aanleg gazon. Instaleren waterdichte verlichting in de steentjes.',
          tag: 'tuin',
          size: ['item--wide', 'item--medium'],
        },
        {
          featured: { img: tuinDegerNa, description: 'Deger Tuin aanleg' },
          title: 'Tuinaanleg JP',
          description: 'Plaatsen van afsluiting en poortjes.',
          tag: 'tuin',
          size: ['item--wide', 'item--large'],
          images: [
            { img: tuinDegerVoor, description: 'Deger Tuin aanleg' },
            {
              img: tuinDegerTijdens1,
              description:
                'Plaatsen van afsluiting, boordstenen, poortjes. Planten van bomen, aanleg gazon. Instaleren waterdichte verlichting in de steentjes.',
            },
            { img: tuinDegerTijdens2, description: 'Deger Tuin aanleg' },
          ],
        },
      ],
    };
  },
};
</script>

<style lang="scss" scoped>
.filters {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  li {
    margin: 5px 10px;
    list-style: none;
    &:hover {
      cursor: pointer;
    }
  }
}
.container {
  width: 100%;
}
.grid {
  display: grid;
  grid-gap: 30px;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  grid-auto-rows: 150px;
  grid-auto-flow: row dense;
}
</style>