<template>
  <button style="height: 5vh; z-index: 60" class="m-2" @click="ModalOpen">
    CreateTask
  </button>
  <section
    v-if="isModal"
    class="bg-white h-100 w-100 position-absolute"
    style="z-index: 20"
    @click="closeModal"
  ></section>
  <section
    v-if="isModal"
    class="position-absolute d-flex justify-content-center align-items-start p-2"
    style="
      z-index: 90;
      left: 20%;
      top: 20%;
      transform: translate(0%, 0%);
      height: 100vh;
      width:50vw
      margin-top: 20vh;
    "
  >
    <form
      class="d-flex flex-column border border-dark p-2 border-3 h-50 position-absolute"
      @submit.prevent="addTask"
    >
      <input
        class="border rounded p-2 mb-2"
        v-model.lazy="newTask.title"
        placeholder="Title"
        type="text"
      />
      <textarea
        ref="texsearch"
        rows="20"
        class="border rounded p-2 mb-2"
        v-model.lazy="newTask.description"
        placeholder="Task Details"
        type="text"
      ></textarea>
      <button
        class="border rounded p-2 bg-success text-white"
        type="submit"
        @submit.prevent=""
      >
        New Task
      </button>
    </form>
  </section>
</template>

<script>

export default {
  inheritAttrs: false,
  name: "CreateTask",
  props: ["tasker"],
  data() {
    return {
      isModal: false,
      newTask: {
        title: "",
        description: "",
      },
    };
  },
  methods: {
    ModalOpen() {
      this.isModal = true;
    },
    closeModal() {
      this.isModal = false;
    },
    addTask() {
      if (this.newTask.title && this.newTask.description) {
        this.$emit("new-task", this.newTask);
        this.isModal = false;
      }
    },
    showModal() {
      this.isModal = true;
      // auto focus
      this.$nextTick(() => {
        this.$refs.textsearch.focus();
      });
    },
  },
};
</script>

<style>
</style>