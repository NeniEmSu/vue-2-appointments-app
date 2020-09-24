<template>
  <div id="app" class="container">
    <h1>{{ title }}</h1>
    <AddAppointment @add="addApt" />
    <SearchAppointments
      :myKey="filterKey"
      :myDir="filterDir"
      @searchRecords="searchApt"
      @update-key="updateKey"
      @update-dir="updateDir"
    />
    <AppointmentList
      :appointments="filteredApt"
      :loading="loading"
      :errror="error"
      @remove="removeRecord"
      @edit="editItem"
    />
  </div>
</template>

<script>
import axios from "axios";
import _ from "lodash";
import AppointmentList from "./components/AppointmentList.vue";
import AddAppointment from "./components/AddAppointment";
import SearchAppointments from "./components/SearchAppointments";

export default {
  name: "App",
  components: { AppointmentList, AddAppointment, SearchAppointments },
  data() {
    return {
      title: "Appointment List",
      appointments: [],
      aptIndex: 0,
      loading: false,
      error: "",
      searchTerms: "",
      filterKey: "petName",
      filterDir: "asc",
    };
  },
  mounted() {
    this.getAppointments();
  },
  computed: {
    searchedApt() {
      return this.appointments.filter((item) => {
        return (
          item.petName.toLowerCase().match(this.searchTerms.toLowerCase()) ||
          item.petOwner.toLowerCase().match(this.searchTerms.toLowerCase()) ||
          item.aptNotes.toLowerCase().match(this.searchTerms.toLowerCase())
        );
      });
    },

    filteredApt() {
      return _.orderBy(
        this.searchedApt,
        (item) => {
          return item[this.filterKey].toLowerCase();
        },
        this.filterDir
      );
    },
  },
  methods: {
    addApt(formData) {
      formData.aptId = this.aptIndex;
      this.aptIndex++;
      this.appointments.push(formData);
    },
    editItem(id, field, text) {
      const itemIndex = this.appointments.findIndex(
        (item) => item.aptId === id
      );
      this.appointments[itemIndex][field] = text;
    },
    searchApt(terms) {
      this.searchTerms = terms;
    },
    updateKey(value) {
      this.filterKey = value;
    },
    updateDir(value) {
      this.filterDir = value;
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
