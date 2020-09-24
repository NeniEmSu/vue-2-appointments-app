<template>
  <div id="app" class="container">
    <h1>{{ title }}</h1>
    <b-icon-plus></b-icon-plus><span>Add appointment</span>
    <div class="appointments" v-for="(appointment, index) in appointments" :key="index">
      <div class="appointments-list"><h3>{{ appointment.petName }}</h3>
      <p>{{ appointment.aptNotes }}</p></div>
    </div>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: "App",
  components: {},
  data() {
    return {
      title: "Appointment List",
      appointments: [
        {
          petName: "Spot",
          petOwner: "Constance Smith",
          aptDate: "2017-07-24 08:30",
          aptNotes: "This German Shepherd is having some back pain",
        },
        {
          petName: "Goldie",
          petOwner: "Barot Bellingham",
          aptDate: "2017-07-22 15:50",
          aptNotes: "This Goldfish has some weird spots in the belly",
        },
        {
          petName: "Mitten",
          petOwner: "Hillary Goldwyn",
          aptDate: "2017-07-21 9:15",
          aptNotes: "Cat has excessive hairballs",
        },
        {
          petName: "Buffy",
          petOwner: "Hassum Harrod",
          aptDate: "2017-07-20 15:30",
          aptNotes:
            "This Chihuahua has not eaten for three days and is lethargic",
        },
      ],
    };
  },
  methods: {
    getAppointments(){
      this.$axios.get("https://gist.githubusercontent.com/planetoftheweb/46426d47f21f2c9245bbe23f0fb834b5/raw/afae0adf97472893288ac5cde69e7bbb770793ed/appointments.json",)
    }
  }
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
