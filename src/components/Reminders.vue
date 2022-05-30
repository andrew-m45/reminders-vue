<template>
  <ul
    class="list"
    @dblclick="$emit('toggle-alert', reminder.id)"
    :key="reminder.id"
    v-for="reminder in reminders"
  >
    <!-- create list item for every reminder -->
    <li>
      <!-- render reminder content component for each reminder -->
      <!-- emits custom event to parent component to delete reminder -->
      <ReminderContent
        @delete-reminder="$emit('delete-reminder', reminder.id)"
        :reminder="reminder"
      />
    </li>
  </ul>
</template>

<script>
// import reminder content component
import ReminderContent from "./ReminderContent.vue";

export default {
  name: "Todos",
  // recieveing reminders array as a prop
  props: {
    reminders: Array,
  },
  components: { ReminderContent },
  // array of emitted events in the component
  emits: ["delete-reminder", "toggle-alert"],
};
</script>
