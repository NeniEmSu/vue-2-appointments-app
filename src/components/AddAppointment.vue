<template>
  <div class="col-12">
    <div class="card textcenter mt-3">
      <div
        class="card-header bg-primary text-white"
        @click="hidePanel = !hidePanel"
      >
        <b-icon-plus font-scale="1.5" class="mr-3" />Add Appointment
      </div>

      <div class="card-body" :class="{ 'd-none': hidePanel }">
        <form id="aptForm" @submit.prevent="requestAdd">
          <div class="form-group form-row">
            <label class="col-md-2 col-form-label text-md-right" for="petName"
              >Pet Name</label
            >
            <div class="col-md-10">
              <input
                type="text"
                class="form-control"
                name="petName"
                id="petName"
                v-model="formData.petName"
                placeholder="Pet's Name"
              />
            </div>
          </div>

          <div class="form-group form-row">
            <label class="col-md-2 col-form-label text-md-right" for="ownerName"
              >Pet Owner</label
            >
            <div class="col-md-10">
              <input
                type="text"
                class="form-control"
                id="ownerName"
                v-model="formData.petOwner"
                placeholder="Owner's Name"
              />
            </div>
          </div>

          <div class="form-group form-row">
            <label class="col-md-2 col-form-label text-md-right" for="aptDate"
              >Date</label
            >
            <div class="col-md-4">
              <input
                type="date"
                class="form-control"
                id="aptDate"
                v-model="formData.aptDate"
              />
            </div>
            <label class="col-md-2 col-form-label text-md-right" for="aptTime"
              >Time</label
            >
            <div class="col-md-4">
              <input
                type="time"
                class="form-control"
                name="aptTime"
                id="aptTime"
                v-model="formData.aptTime"
              />
            </div>
          </div>

          <div class="form-group form-row">
            <label class="col-md-2 text-md-right" for="aptNotes"
              >Apt. Notes</label
            >
            <div class="col-md-10">
              <textarea
                class="form-control"
                rows="4"
                cols="50"
                name="aptNotes"
                id="aptNotes"
                v-model="formData.aptNotes"
                placeholder="Appointment Notes"
              ></textarea>
            </div>
          </div>

          <div class="form-group form-row mb-0">
            <div class="offset-md-2 col-md-10">
              <button type="submit" class="btn btn-primary d-block ml-auto">
                Add Appointment
              </button>
            </div>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
// import axios from "axios";
export default {
  name: "AddAppointment",
  data() {
    return {
      formData: {},
      hidePanel: true,
    };
  },
  methods: {
    requestAdd() {
      this.formData = {
        petName: this.formData.petName,
        petOwner: this.formData.petOwner,
        aptDate: `${this.formData.aptDate} ${this.formData.aptTime}`,
        aptNotes: this.formData.aptNotes,
      };
      this.$emit('add', this.formData)
      this.formData = {}
      this.hidePanel = true
    },
  },
};
</script>

<style lang="scss" scoped>
.card-header {
  cursor: pointer;
}
</style>