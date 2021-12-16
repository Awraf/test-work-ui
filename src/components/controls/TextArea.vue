<template>
  <div>
    <label :for="id" :class="{ red: !isValid }">
      <span v-if="isRequired">*</span>
      {{ title }}
    </label>
    <textarea
      :id="id"
      cols="30"
      rows="5"
      :class="{ red: !isValid }"
      v-on:keyup="emitValue"
    ></textarea>
    <ErrorMessage :message="errorMessage" v-if="!isValid" />
  </div>
</template>

<script>
import ErrorMessage from "@/components/controls/ErrorMessage";

export default {
  components: {
    ErrorMessage
  },
  props: {
    id: String,
    isRequired: Boolean,
    title: String,
    isValid: Boolean,
    errorMessage: String,
  },
  methods: {
    emitValue(event) {
      this.$emit("changed", event.target.value);
    },
  },
};
</script>

<style scoped>
textarea {
  display: block;
  width: 240px;
  margin-bottom: 8px;
}

.red {
  border-color: var(--color-red);
  color: var(--color-red);
}
</style>