<template>
  <!-- classes applied according to the alert status -->

  <div :class="[reminder.alert ? 'priority' : 'normal', 'content']">
    <!-- dbl click event emitted to change the alert status -->
    <div @dblclick="$emit('toggle-alert', reminder.id)" class="left">
      <h1>{{ reminder.text }}</h1>
      <p>{{ reminder.day }} {{ reminder.time }}</p>
    </div>
    <!-- emits a custom event to reminders component -->
    <button @click="onDelete(reminder.id)">
      <i class="far fa-trash-alt"></i>
    </button>
  </div>
</template>

<script>
export default {
  name: "ReminderContent",
  props: {
    reminder: Object,
  },
  methods: {
    //custom event to the reminders component with reminder id
    onDelete(id) {
      this.$emit("delete-reminder", id);
    },
  },
  // array of emitted events in the component
  emits: ["toggle-alert", "delete-reminder"],
};
</script>

<style scoped>
button {
  border: none;
  outline: none;
  border-radius: 50%;
  cursor: pointer;
}
</style>
