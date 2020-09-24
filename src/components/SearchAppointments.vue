<template>
  <div class="search-appointments row justify-content-center my-4">
    <div class="col-md-6">
      <div class="input-group">
        <input
          id="SearchApts"
          type="text"
          class="form-control"
          aria-label="Search Appointments"
          v-model="searchTerm"
        />
        <div class="input-group-append">
          <b-dropdown
            id="dropdown-1"
            text="Sort by:"
            class="sort-menu dropdown-menu-right"
          >
            <b-dropdown-item @click="$emit('update-key', 'petName')"
              >Pet Name
              <b-icon-check
                v-if="myKey === 'petName'"
                class="ml-2"
              ></b-icon-check
            ></b-dropdown-item>
            <b-dropdown-item @click="$emit('update-key', 'aptDate')"
              >Date
              <b-icon-check
                v-if="myKey === 'aptDate'"
                class="ml-2"
              ></b-icon-check
            ></b-dropdown-item>
            <b-dropdown-item @click="$emit('update-key', 'petOwner')"
              >Owner
              <b-icon-check
                v-if="myKey === 'petOwner'"
                class="ml-2"
              ></b-icon-check
            ></b-dropdown-item>
            <b-dropdown-divider></b-dropdown-divider>
            <b-dropdown-item @click="$emit('update-dir', 'asc')"
              >Asc
              <b-icon-check v-if="myDir === 'asc'" class="ml-2"></b-icon-check
            ></b-dropdown-item>
            <b-dropdown-item @click="$emit('update-dir', 'desc')"
              >Desc
              <b-icon-check v-if="myDir === 'desc'" class="ml-2"></b-icon-check
            ></b-dropdown-item>
          </b-dropdown>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "SearchAppointments",
  props: {
    myKey: {
      default: "petName",
      type: String,
    },
    myDir: {
      default: "asc",
      type: String,
    },
  },
  data() {
    return {
      searchTerm: "",
    };
  },
  watch: {
    searchTerm() {
      this.$emit("searchRecords", this.searchTerm);
    },
  },
};
</script>

<style lang="scss" scoped>
</style>