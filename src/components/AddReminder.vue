<template>
  <!-- Modal -->
  <div
    class="modal fade"
    id="addReminder"
    tabindex="-1"
    role="dialog"
    aria-labelledby="addReminderLabel"
    aria-hidden="true"
  >
    <div class="modal-dialog" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">Add New Reminder</h5>
          <button
            type="button"
            class="close"
            data-dismiss="modal"
            aria-label="Close"
            @click="$emit('toggle-addReminder')"
          >
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div class="modal-body">
          <form>
            <div class="form-group">
              <label class="col-form-label">Reminder Text</label>
              <input
                placeholder="Add Reminder"
                type="text"
                class="form-control"
                id="reminder-text"
                v-model="text"
              />
            </div>
            <div class="form-group">
              <label class="col-form-label">Day</label>
              <input
                placeholder="Add Reminder Day"
                type="text"
                class="form-control"
                id="reminder-day"
                v-model="day"
              />
            </div>
            <div class="form-group">
              <label class="col-form-label">Time</label>
              <input
                placeholder="Add Reminder Time"
                type="text"
                class="form-control"
                id="reminder-time"
                v-model="time"
              />
            </div>
            <label class="col-form-label">Choose Reminder Status</label>
            <br />

            <div class="form-check form-check-inline">
              <input
                class="form-check-input"
                type="checkbox"
                id="priority-check"
                value="true"
                v-model="alert"
              />
              <label class="form-check-label" for="priority-check"
                >Priority</label
              >
            </div>
          </form>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-primary" @click="handleSubmit">
            Add Reminder
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "AddReminder",
  data() {
    return {
      text: "",
      day: "",
      time: "",
      alert: false,
    };
  },
  methods: {
    handleSubmit(e) {
      // prevent default submit action
      e.preventDefault();

      // validation for empty form field
      if (!this.text || !this.day || !this.time) {
        alert("Please complete the form and try again!");
      } else {
        // new reminder object
        const newReminder = {
          text: this.text,
          day: this.day,
          time: this.time,
          alert: this.alert,
        };

        // emit the object to parent component
        this.$emit("add-reminder", newReminder);

        // reset form
        this.text = "";
        this.day = "";
        this.time = "";
        this.alert = false;
      }
    },
  },
};
</script>

<style></style>
