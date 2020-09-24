<template>
  <div id="app" class="container">
    <h1>{{ title }}</h1>
    <b-icon-plus></b-icon-plus><span>Add appointment</span>
    <AppointmentList />
  </div>
</template>

<script>
import AppointmentList from "./components/AppointmentList.vue";

export default {
  name: "App",
  components: { AppointmentList },
  data() {
    return {
      title: "Appointment List",
    };
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin-top: 60px;
}
</style>
