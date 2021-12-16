<template>
  <div>
    <div v-for="(data, index) of selectedData" :key="index">
      <input
        type="radio"
        :value="data.value || data.title"
        :name="groupName"
        :id="data.id"
        :checked="data.isDefault"
        @change="changed"
        class="custom-radio"
      />
      <label :for="data.id">{{ data.title }}</label>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    selectedData: Array,
    groupName: String,
  },
  methods: {
    changed($event) {
      this.$emit("changed", $event.target.value);
    },
  },
};
</script>

<style scoped>
label {
  display: inline-block;
  vertical-align: top;
  margin: 3px 3px 0 3px;
  text-transform: uppercase;
}

input {
  z-index: -1;
  margin: 3px 3px 0 3px;
}
.custom-radio {
  position: absolute;
  z-index: -1;
  opacity: 0;
}

.custom-radio + label {
  display: inline-flex;
  align-items: center;
  user-select: none;
}

.custom-radio + label::before {
  content: "";
  display: inline-block;
  width: 1em;
  height: 1em;
  flex-shrink: 0;
  flex-grow: 0;
  border: 1px solid #000000;
  border-radius: 50%;
  margin-right: 0.5em;
  background-repeat: no-repeat;
  background-position: center center;
  background-size: 50% 50%;
}
.custom-radio:checked + label::before {
  border-color: #000000;
  background-color: #ffffff;
  background-image: url("data:image/svg+xml,%3Csvg width='4' height='4' viewBox='0 0 4 4' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Ccircle cx='2' cy='2' r='2' fill='%23FF0000'/%3E%3C/svg%3E");
}
</style>
