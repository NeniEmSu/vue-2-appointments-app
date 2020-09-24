<template>
  <div id="app" class="container">
    <h1>{{ title }}</h1>
    <AddAppointment @add="addApt" />
    <AppointmentList :appointments="appointments" :loading="loading" :errror="error" @remove="removeRecord" @edit="editItem"/>    
  </div>
</template>

<script>
import axios from "axios";
import AppointmentList from "./components/AppointmentList.vue";
import AddAppointment from './components/AddAppointment';

export default {
  name: "App",
  components: { AppointmentList, AddAppointment },
   data() {
    return {
      title: "Appointment List",
      appointments: [],
      loading: false,
      error: "",
      aptIndex: 0,
    };
  },
  mounted() {
    this.getAppointments();
  },
  methods: {
    addApt(formData){
      formData.aptId = this.aptIndex
      this.aptIndex++
      this.appointments.push(formData)
    },
    editItem(id, field, text){
        const itemIndex = this.appointments.findIndex(item => item.aptId === id)
        this.appointments[itemIndex][field ]= text        
    },
    removeRecord(item) {
      this.appointments = this.appointments.filter((elm) => elm !== item);
      //   Or using lodash
      //   this.appointments = _.without(this.appointments, item)
    },
    async getAppointments() {
      this.loading = true;
      try {
        const RESPONSE = await axios.get(
          "https://gist.githubusercontent.com/planetoftheweb/46426d47f21f2c9245bbe23f0fb834b5/raw/afae0adf97472893288ac5cde69e7bbb770793ed/appointments.json"
        );
        this.appointments = RESPONSE.data.map((item) => {
          item.aptId = this.aptIndex;
          this.aptIndex++;
          return item;
        });
      } catch (error) {
        this.error = error;
      } finally {
        this.loading = false;
      }
    },
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
