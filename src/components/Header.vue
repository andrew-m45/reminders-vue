<template>
  <div class="wrapper">
    <div class="app__header">
      <h1>{{ title }}</h1>
      <p>Easy & Simple Reminders App</p>
    </div>
    <button
      @click="toggleAddReminder"
      data-toggle="modal"
      data-target="#addReminder"
    >
      <i class="fas fa-plus"></i>
    </button>
  </div>
</template>

<script>
export default {
  name: "Header",
  props: {
    title: String,
  },
  methods: {
    toggleAddReminder() {
      this.$emit("toggle-addReminder");
    },
  },
};
</script>

<style scoped>
.wrapper {
  display: flex;
}

.app__header {
  flex: 2;
}

h1 {
  color: #333;
  font-size: 1.8rem;
  line-height: 35px;
}

p {
  color: #666;
  margin-bottom: 0.5rem;
}

button {
  border: none;
  outline: none;
  background: none;
  padding: 5px 5px;
}

i {
  cursor: pointer;
  color: #fff;
  padding: 10px;
  border-radius: 50%;
  font-size: 1.5rem;
  background: var(--primary-color);
  box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
}
</style>
