<template>
  <div class="container">
    <div
      class="card"
      :class="
        noteProps.status === 'TO DO'
          ? 'card-todo'
          : noteProps.status === 'DOING'
          ? 'card-doing'
          : 'card-done'
      "
    >
      <div class="card-header">
        <el-tooltip
          class="item"
          effect="dark"
          :content="noteProps.title"
          placement="top-start"
        >
          <span class="card-title">{{ noteProps.title }}</span>
        </el-tooltip>
        <span class="card-action-btn"
          ><ActionButton
            :noteProps="noteProps"
            @deleteNote="deleteNote($event)"
            @editNote="editNote($event)"
        /></span>
      </div>
      <hr />
      <div class="card-body">
        <div class="card-status">
          <StatusBadge :noteProps="noteProps" />
        </div>
        <hr />
        <el-tooltip
          class="item"
          effect="dark"
          :content="noteProps.description"
          placement="bottom"
        >
          <div class="card-content">{{ noteProps.description }}</div>
        </el-tooltip>
      </div>
    </div>
  </div>
</template>

<script>
import ActionButton from "./ActionButton.vue";
import StatusBadge from "./StatusBadge.vue";
export default {
  name: "SingleCard",
  components: {
    ActionButton,
    StatusBadge,
  },
  props: ["noteProps"],
  data() {
    return {};
  },
  methods: {
    editNote(data) {
      this.$emit("editNote", data);
    },
    deleteNote(data) {
      this.$emit("deleteNote", data);
    },
  },
};
</script>

<style scoped>
.container {
  padding: 30px;
}
.card {
  border: 2px solid rgb(83, 191, 157);
  width: 300px;
  height: 200px;
  padding: 0 10px;
  border-radius: 2px;
}

.card-todo {
  border: 2px solid rgb(255, 120, 120);
}
.card-doing {
  border: 2px solid rgb(255, 165, 0);
}
.card-done {
  border: 2px solid rgb(83, 191, 157);
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 2px;
  margin: 10px 0;
}

.card-title {
  font-size: 18px;
  text-align: left;
  width: 150px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

hr {
  border: none;
  height: 2px;
  background: rgb(198, 198, 198);
}

.card-body {
  margin: 10px 0;
}

.card-content {
  display: block;
  margin: 10px 0;
  text-align: justify;
  height: 70px;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 4;
  -webkit-box-orient: vertical;
  cursor: default;
}
</style>
