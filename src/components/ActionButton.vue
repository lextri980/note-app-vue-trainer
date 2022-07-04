<template>
  <div class="action-btn-container">
    <el-link
      :href="noteProps.url"
      target="_blank"
      :underline="false"
      class="action-btn link-btn"
      icon="el-icon-link"
      :disabled="!noteProps.url"
    ></el-link>
    <el-button
      type="warning"
      icon="el-icon-edit"
      circle
      class="action-btn"
      @click="handleEdit"
    ></el-button>
    <el-button
      type="danger"
      icon="el-icon-delete"
      circle
      class="action-btn"
      @click="handleDelete"
    ></el-button>
  </div>
</template>

<script>
export default {
  name: "ActionButton",
  props: ["noteProps"],
  data() {
    return {};
  },
  methods: {
    handleEdit() {
      this.$emit("editNote", {
        noteProps: this.noteProps,
      });
    },
    handleDelete() {
      this.$emit("deleteNote", { id: this.noteProps.id });
    },
  },
};
</script>

<style scoped>
.action-btn {
  padding: 8px !important;
}
.link-btn {
  background: #d3ebcd;
  color: white;
  border-radius: 50px;
  font-size: 17px;
  margin-right: 10px;
}
</style>
