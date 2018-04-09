<template>
  <div id="app">
    <project v-for="(project, i) in projects" :key="i" :project="project" v-on:showSlideshow="showSlideshow" />
    <slideshow v-if="slideshow" :images="images" v-on:hideSlideshow="hideSlideshow" />
  </div>
</template>

<script>
import Project from './components/Project';
import Slideshow from './components/Slideshow';
import axios from 'axios';

export default {
  name: 'app',
  components: {
    Project,
    Slideshow,
  },
  methods: {
    showSlideshow(images) {
      this.images = images;
      this.slideshow = true;
    },
    hideSlideshow() {
      this.slideshow = false;
      this.images = [];
    },
  },
  data() {
    return {
      slideshow: false,
      images: [],
      projects: [],
    };
  },
  created: function() {
    axios.get('js/projects.json').then(response => {
      this.projects = response.data;
    });
  },
};
</script>