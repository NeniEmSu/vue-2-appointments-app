<template>
  <div>
    <template v-if="loading">
      <div class="loading"><h2>Loading...</h2></div>
    </template>
    <template v-else-if="appointments.length > 0">
      <div
        class="appointments"
        v-for="(appointment, index) in appointments"
        :key="index"
      >
        <div class="appointments-list">
          <h3>{{ appointment.petName }}</h3>
          <p>{{ appointment.aptNotes }}</p>
        </div>
      </div>
    </template>
    <template v-else>
      <div class="error">
        <h2>An error occured while fetching data:</h2>
        <p>{{ error }}</p>
      </div>
    </template>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "AppointMentList",
  data() {
    return {
      appointments: [],
      loading: false,
      error: {},
    };
  },
  mounted() {
    this.getAppointments();
  },
  methods: {
    async getAppointments() {
      this.loading = true;
      try {
        const RESPONSE = await axios.get(
          "https://gist.githubusercontent.com/planetoftheweb/46426d47f21f2c9245bbe23f0fb834b5/raw/afae0adf97472893288ac5cde69e7bbb770793ed/appointments.json"
        );
        this.appointments = RESPONSE.data;
      } catch (error) {
        this.error = error;
      } finally {
        this.loading = false;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
</style>