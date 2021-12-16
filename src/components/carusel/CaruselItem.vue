<template>
  <transition name="fade">
    <div
      class="slider-item-container"
      :class="{ active: isActive, inactive: !isActive }"
      :style="getStyles"
    >
      <div
        v-if="isActive"
        class="slider-item"
        :style="{ backgroundColor: color }"
      ></div>
      <div
        v-else
        class="slider-preview"
        :style="{ backgroundColor: color }"
      ></div>
    </div>
  </transition>
</template>

<script>
export default {
  props: {
    color: String,
    index: Number,
    position: Number,
    isActive: Boolean,
  },
  mounted() {
    this.$nextTick(() => {
      window.addEventListener("resize", this.onResize);
    });
  },
  data() {
    return {
      windowWidth: window.innerWidth,
    };
  },
  computed: {
    getStyles() {
      return {
        "z-index": this.isActive ? 10 : this.position,
        width: `calc(100% - ${this.position} * ${this.windowWidth > 1200 ? '37px': '19px'})`,
      };
    },
  },
  beforeDestroy() {
    window.removeEventListener("resize", this.onResize);
  },

  methods: {
    onResize() {
      this.windowWidth = window.innerWidth;
    },
  },
};
</script>

<style>
.slider-item-container {
  position: absolute;
  height: var(--slider-height);
}

.slider-item {
  height: 100%;
  position: relative;
  border-top-right-radius: var(--slider-item--border-radius);
  border-bottom-right-radius: var(--slider-item--border-radius);
}

.active {
  transition: all 1.2s ease-in;
}

.inactive {
  transition: all 1.2s ease-in;
}

.slider-preview {
  height: 100%;
  border-top-right-radius: var(--slider-item--border-radius);
  border-bottom-right-radius: var(--slider-item--border-radius);
}

@media only screen and (max-width: 1220px) {
  .slider-item-container {
    height: var(--slider-mobile-height);
  }
}
</style>