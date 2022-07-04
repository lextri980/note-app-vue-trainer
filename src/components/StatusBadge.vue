<template>
  <div class="status-badge-container">
    <span
      class="pill"
      :class="[noteProps.status === 'TO DO' ? 'todo' : 'todo-disable']"
      >TO DO</span
    >
    <span
      class="pill"
      :class="[noteProps.status === 'DOING' ? 'doing' : 'doing-disable']"
      >DOING</span
    >
    <span
      class="pill"
      :class="[noteProps.status === 'DONE' ? 'done' : 'done-disable']"
      >DONE</span
    >
  </div>
</template>

<script>
export default {
  name: "StatusBadge",
  props: ["noteProps"],
};
</script>

<style scoped>
.status-badge-container {
  display: flex;
  margin-bottom: 10px;
  display: flex;
  justify-content: space-between;
}
.pill {
  padding: 7px;
  border-radius: 50px;
  font-size: 12px;
  font-weight: bold;
  color: white;
  width: 80px;
  cursor: default;
}

.todo {
  background: rgb(255, 120, 120);
}
.todo-disable {
  background: rgb(255, 120, 120, 0.1);
}
.doing {
  background: rgb(255, 165, 0);
}
.doing-disable {
  background: rgb(255, 165, 0, 0.1);
}
.done {
  background: rgb(83, 191, 157);
}
.done-disable {
  background: rgb(83, 191, 157, 0.1);
}
</style>
