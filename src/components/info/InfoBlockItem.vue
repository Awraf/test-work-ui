<template>
  <div class="info-item">
    <div class="image-left" v-if="imageLeft">
      <img :src="getImageSrc()" :alt="title" />
    </div>
    <div class="info">
      <h2>{{ title }}</h2>
      <p>{{ description }}</p>
    </div>
    <div class="image-right" v-if="!imageLeft">
      <img :src="getImageSrc()" :alt="title" />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    poster: String,
    title: String,
    description: String,
    imageLeft: Boolean,
  },
  methods: {
    getImageSrc() {
      return `https://image.tmdb.org/t/p/w185_and_h278_bestv2${this.poster}`;
    },
  },
};
</script>

<style scoped>
.info-item {
  background-color: var(--background-grey);
  padding: 28px 32px;
  margin: 37px 5%;
  min-width: 320px;
  display: flex;
  flex-basis: fit-content;
}

.image-left,
.image-right {
  display: flex;
  align-items: center;
}

.info {
  display: flex;
  flex-direction: column;
  flex-basis: fit-content;
  padding: 25px;
}

p {
  font-size: 14px;
  line-height: 15px;
  font-style: normal;
  font-weight: 400;
}

h2 {
  font-size: 30px;
  /* line-height: 64px; */
  font-style: normal;
  font-weight: 400;
}
</style>