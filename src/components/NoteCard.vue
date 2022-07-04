<template>
  <div class="notecard-container">
    <div class="single-card">
      <SingleCard
        v-for="note in notes"
        :key="note.id"
        :noteProps="note"
        :editForm="editForm"
        :openModal="openModal"
        @deleteNote="deleteNote($event)"
        @editNote="editNote($event)"
      />
    </div>
    <!-- //? Create btn -->
    <span class="create-btn-wrapper">
      <el-tooltip
        class="item"
        effect="dark"
        content="Create note"
        placement="left"
      >
        <el-button
          type="success"
          icon="el-icon-plus"
          circle
          class="create-btn"
          @click="openModalUp"
        ></el-button>
      </el-tooltip>
    </span>
    <!-- //? Create Update modal -->
    <el-dialog
      :title="editForm === false ? 'Create new note' : 'Update note'"
      :visible.sync="openModal"
      width="450px"
      :close-on-click-modal="false"
      :show-close="false"
    >
      <form @submit="onSubmit">
        <span class="dialog-body">
          <el-input
            placeholder="Enter title"
            v-model="noteItems.title"
            clearable
            class="mb-15"
          />
          <el-input
            type="textarea"
            :rows="3"
            placeholder="Enter description"
            v-model="noteItems.description"
            class="mb-15"
          >
          </el-input>
          <el-input
            placeholder="Enter URL"
            v-model="noteItems.url"
            clearable
            class="mb-15"
          />
          <el-select
            v-model="noteItems.status"
            class="full-width"
            v-if="editForm === true"
          >
            <el-option
              v-for="item in options"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            >
            </el-option>
          </el-select>
        </span>
        <hr />
        <span class="dialog-footer">
          <el-button type="danger" @click="cleanModal">Cancel</el-button>
          <el-button type="success" native-type="submit">{{
            editForm === false ? "Create" : "Update"
          }}</el-button>
        </span>
      </form>
    </el-dialog>
  </div>
</template>

<script>
import SingleCard from "./SingleCard.vue";
import { notes } from "../data";
import { v4 } from "uuid";

export default {
  name: "NoteCard",
  components: { SingleCard },
  data() {
    const visible = true;
    let openModal = false;
    let editForm = false;
    const noteItems = {
      id: "",
      title: "",
      description: "",
      url: "",
      status: "",
    };
    const options = [
      {
        value: "TO DO",
        label: "TO DO",
      },
      {
        value: "DOING",
        label: "DOING",
      },
      {
        value: "DONE",
        label: "DONE",
      },
    ];

    return {
      visible,
      notes,
      openModal,
      editForm,
      noteItems,
      options,
    };
  },
  methods: {
    cleanModal() {
      this.openModal = false;
      this.noteItems = {
        title: "",
        description: "",
        url: "",
        status: "",
      };
      this.editForm = false;
    },

    onSubmit(e) {
      e.preventDefault();
      if (this.editForm === false) {
        if (
          this.noteItems.title.trim() !== "" &&
          this.noteItems.description.trim() !== ""
        ) {
          const newNote = {
            id: v4(),
            title: this.noteItems.title,
            description: this.noteItems.description,
            url: this.noteItems.url,
            status: "TO DO",
          };
          notes.unshift(newNote);
        }
      } else {
        const updatedNote = {
          id: this.noteItems.id,
          title: this.noteItems.title,
          description: this.noteItems.description,
          url: this.noteItems.url,
          status: this.noteItems.status,
        };
        const updateItems = notes.map((note) => {
          return note.id === updatedNote.id ? updatedNote : note;
        });

        this.notes = updateItems;
      }
      this.cleanModal();
    },

    deleteNote(data) {
      const confirmDelete = confirm("Do you want to delete this note?");
      if (confirmDelete === true) {
        this.notes = this.notes.filter((note) => note.id !== data.id);
      } else {
        return;
      }
    },

    editNote(data) {
      this.editForm = true;
      this.openModal = true;
      this.noteItems = { ...data.noteProps };
    },

    openModalUp() {
      this.openModal = true;
      console.log(this.editForm);
    },
  },
};
</script>

<style scoped>
.notecard-container {
  display: flex;
  justify-content: center;
  align-items: center;
}
.create-btn {
  padding: 17px !important;
  position: fixed;
  bottom: 40px;
  right: 40px;
}
.single-card {
  width: 100vw;
  display: flex;
  flex-wrap: wrap;
}
.dialog-footer {
  display: flex;
  justify-content: flex-end;
}

hr {
  border: none;
  height: 1px;
  background: rgb(198, 198, 198);
  margin: 20px 0;
}

.mb-15 {
  margin-bottom: 15px;
}

.full-width {
  width: 100%;
}
</style>
