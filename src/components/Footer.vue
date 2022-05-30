<template>
  <div class="info">
    <p>
      You have <span id="num">{{ reminders.length }}</span> incompelete tasks
    </p>
    <button @click="$emit('delete-all')" id="clear">Clear All</button>
  </div>
</template>

<script>
export default {
  name: "Footer",
  props: {
    reminders: Array,
  },
  emits: ["delete-all"],
};
</script>

<style scoped>
.info {
  margin-top: 20px;
  position: relative;
  top: 15px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.info p {
  position: relative;
  top: 6px;
}

.info span {
  font-weight: 700;
  color: var(--primary-color);
}

.info button {
  border: none;
  outline: none;
  background: var(--primary-color);
  padding: 6px 18px;
  border-radius: 5px;
  color: #fff;
  cursor: pointer;
  font-weight: 500;
  font-size: 15px;
  box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
}
</style>
