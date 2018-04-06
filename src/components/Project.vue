<template>
  <div class="item" @click="$emit('showSlideshow', images)">
    <img :src="items.featured.img" alt="Image" />
    <div class="item_text">
      <p>{{ items.title }}
        <span> {{ items.description }}</span>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  props: ['items'],
  data() {
    return {
      images: [],
    };
  },
  mounted() {
    this.images.push(this.items.featured);
    if (this.items.images) this.images = this.images.concat(this.items.images);
  },
};
</script>

<style lang="scss" scoped>
img {
  width: 100%;
}
.item {
  position: relative;
  box-sizing: border-box;
  grid-column-start: auto;
  grid-row-start: auto;

  &:hover {
    cursor: pointer;
  }
  &--medium {
    grid-row-end: span 2;
  }

  &--wide {
    grid-column-end: span 2;
  }

  &--large {
    grid-row-end: span 3;
  }

  &--full {
    grid-column-end: auto;

    @media screen and (min-width: 768px) {
      grid-column: 1/-1;
      grid-row-end: span 2;
    }
  }

  &_text {
    display: none;
  }
}
</style>

