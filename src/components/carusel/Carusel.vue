<template>
  <div class="slider-container">
    <CaruselItem
      v-for="(color, index) of colors"
      :key="index"
      :isActive="isActive(index)"
      :color="color"
      :index="index"
      :position="getPosition(index)"
    >
    </CaruselItem>
    <CaruselItemContent
      :activeIndex="activeIndex + 1"
      :count="colors.length"
      @next="nextSlide"
    />
  </div>
</template>

<script>
import CaruselItem from "@/components/carusel/CaruselItem";
import CaruselItemContent from "@/components/carusel/CaruselItemContent";

export default {
  props: {
    colors: Array,
  },
  components: {
    CaruselItem,
    CaruselItemContent,
  },
  data() {
    return { activeIndex: 0 };
  },
  methods: {
    isActive(index) {
      return index === this.activeIndex;
    },
    getPosition(index) {
      const length = this.colors.length - 1;
      if (index === this.activeIndex) {
        return length;
      }
      if (index < this.activeIndex) {
        return length - (this.activeIndex - index);
      }
      return length - index;
    },
    nextSlide() {
      if (this.activeIndex === this.colors.length - 1) {
        this.activeIndex = 0;
        return;
      }
      this.activeIndex++;
    },
  },
};
</script>

<style scoped>
.slider-container {
  position: relative;
  height: var(--slider-height);
  min-width: var(--slider-win-width);
}

@media only screen and (max-width: 1220px) {
.slider-container {
  height: var(--slider-mobile-height);
}
}
</style>
