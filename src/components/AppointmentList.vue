<template>
  <div>
    <template v-if="loading">
      <div class="loading">
        <div class="col-12 col-md-10 col-lg-7">
          <div class="list-group list-group-flush">
            <div
              class="list-group-item d-flex"
              v-for="(item, index) in 3"
              :key="index"
            >
              <b-skeleton
                type="button"
                class="mr-2"
                animation="throb"
              ></b-skeleton>
              <div class="w-100">
                <div class="d-flex justify-content-between">
                  <b-skeleton
                    class="mb-3"
                    animation="throb"
                    width="45%"
                  ></b-skeleton>
                  <b-skeleton animation="throb" width="25%"></b-skeleton>
                </div>
                <div class="owner-name">
                  <b-skeleton animation="throb" width="55%"></b-skeleton>
                </div>
                <b-skeleton animation="throb" width="80%"></b-skeleton>
              </div>
            </div>
          </div>
        </div>
      </div>
    </template>
    <template v-else-if="!loading">
      <template v-if="appointments.length < 1">
        <div class="empty">
          <h2>No appointments atm.</h2>
          <p>Have some fun and relax yo.</p>
        </div>
      </template>
      <div v-else class="col-12 col-md-10 col-lg-7">
        <div class="list-group list-group-flush">
          <div
            class="list-group-item d-flex"
            v-for="(appointment, index) in appointments"
            :key="index"
          >
            <button
              class="mr-2 btn btn-sm btn-danger"
              @click="removeRecord(appointment)"
            >
              <b-icon-trash-fill></b-icon-trash-fill>
            </button>
            <div class="w-100">
              <div class="d-flex justify-content-between">
                <span class="h4 text-primary">{{ appointment.petName }}</span>
                <span class="float-right">{{
                  formatDate(appointment.aptDate)
                }}</span>
              </div>
              <div class="owner-name">
                <span class="font-weight-bold text-primary mr-1">Owner:</span>
                <span>{{ appointment.petOwner }}</span>
              </div>
              <div>{{ appointment.aptNotes }}</div>
            </div>
          </div>
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
import moment from "moment";
export default {
  name: "AppointMentList",
  data() {
    return {
      appointments: [],
      loading: false,
      error: "",
    };
  },
  mounted() {
    this.getAppointments();
  },
  methods: {
    formatDate: (date) => {
      return moment(new Date(date)).format("MM-DD-YY, hh:mm a");
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