<template>
  <div id="app">
    <Carusel :colors="colors" />
    <Form />
    <InfoBlocksList />
  </div>
</template>

<script>
import Form from "@/components/form/Form";
import InfoBlocksList from "@/components/info/InfoBlocksList";
import Carusel from "@/components/carusel/Carusel";

export default {
  name: "App",
  components: {
    Form,
    Carusel,
    InfoBlocksList
  },
  data() {
    return {
      colors: ['#027D84', '#4A989A', '#AFB3B4', '#FFB3B4']
    }
  }
};
</script>

<style>
@import "./variables.css";

body {
  margin: 0;
}

h2, p {
  font-family: var(--default-font-family);
}

label {
  font-size: 12px;
  font-family: var(--default-font-family);
  font-weight: 400;
}

div {
  text-align: left;
}
</style>
