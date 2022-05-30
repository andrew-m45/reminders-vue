<template>
  <div class="info">
    <p>
      You have <span id="num">{{ reminders.length }}</span> incompelete tasks
    </p>
  </div>
</template>

<script>
export default {
  name: "Footer",
  props: {
    reminders: Array,
  },
};
</script>

<style scoped>
.info {
  margin-top: 20px;
  position: relative;
  top: 15px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.info p {
  position: relative;
  top: 10px;
}

.info span {
  font-weight: 700;
  color: var(--primary-color);
}
</style>
