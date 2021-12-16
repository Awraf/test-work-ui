<template>
  <div class="input">
    <label :for="id" :class="{ red: !isValid }">
      <span v-if="isRequired">*</span>
      {{ title }}
    </label>
    <input type="text" :id="id" :placeholder="placeholder" :class="{ red: !isValid }" v-on:keyup="emitValue"/>
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
    isValid: Boolean,
    title: String,
    isRequired: Boolean,
    errorMessage: String,
    id: String,
    placeholder: String
  },
  methods: {
    emitValue: function(event) {
      this.$emit("changed", event.target.value);
    },
  },
};
</script>

<style scoped>
.input {
  display: flex;
  flex-direction: column;
}

input {
  height: 31px;
  width: 246px;
  border: 1px solid #000000;
  box-sizing: border-box;
  margin-bottom: 8px;
}

label {
  text-transform: uppercase;
}

.red {
  border-color: var(--color-red);
  color: var(--color-red);
}
</style>