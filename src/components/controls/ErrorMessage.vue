<template>
  <div class="error">
    <span>{{ message }}</span>
  </div>
</template>

<script>
export default {
  props: {
    message: String,
  },
};
</script>

<style scoped>
.error {
  margin-top: -4px;
  margin-bottom: 12px;
  width: 246px;
}

.error span {
  color: var(--color-red);
  font-size: 12px;
}
</style>
