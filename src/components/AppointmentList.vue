<template>
  <div>
    <template v-if="loading">
      <div class="loading">
        <div class="col-12 col-md-10 col-lg-7">
          <div class="list-group list-group-flush">
            <div
              class="list-group-item d-flex align-items-start"
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
            class="list-group-item d-flex align-items-start"
            v-for="appointment in appointments"
            :key="appointment.aptId"
          >
            <button
              class="mr-2 btn btn-sm btn-danger"
              @click="$emit('remove', appointment)"
            >
              <b-icon-trash-fill></b-icon-trash-fill>
            </button>
            <div class="w-100">
              <div class="d-flex justify-content-between">
                <span
                  class="h4 text-primary"
                  contenteditable="contenteditable"
                  @blur="
                    $emit(
                      'edit',
                      appointment.aptId,
                      'petName',
                      $event.target.innerText
                    )
                  "
                  >{{ appointment.petName }}</span
                >
                <time
                  :datetime="formatDateTime(appointment.aptDate)"
                  class="float-right"
                >
                  {{ formatDate(appointment.aptDate) }}
                </time>
              </div>
              <div class="owner-name">
                <span class="font-weight-bold text-primary mr-1">Owner:</span>
                <span
                  contenteditable="contenteditable"
                  @blur="
                    $emit(
                      'edit',
                      appointment.aptId,
                      'petOwner',
                      $event.target.innerText
                    )
                  "
                  >{{ appointment.petOwner }}</span
                >
              </div>
              <div
                contenteditable="contenteditable"
                @blur="
                  $emit(
                    'edit',
                    appointment.aptId,
                    'petNotes',
                    $event.target.innerText
                  )
                "
              >
                {{ appointment.aptNotes }}
              </div>
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
import moment from "moment";
export default {
  name: "AppointMentList",
  props: {
    appointments: {
      default: () => [],
      type: Array,
    },
    loading: {
      default: false,
      type: Boolean,
    },
    error: {
      default: "",
      type: String,
    },
  },
  data() {
    return {};
  },
  methods: {
    formatDate: (date) => {
      const TODAY = new Date();
      const APT_DATE = new Date(date);
      if (TODAY < APT_DATE) return moment(APT_DATE).format("MM-DD-YY, hh:mm a");
      else return moment(APT_DATE).fromNow();
    },
    formatDateTime: (date) => {
      return moment(new Date(date)).format("YYYY-MM-DDTHH:mm");
    },
  },
};
</script>

<style lang="scss" scoped>
</style>