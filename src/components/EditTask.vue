<template>
  <section
    v-if="bool"
    :tasker="taskers"
    class="bg-success h-100 w-100 position-absolute"
    style="z-index: 70; width: 100vw; top: 15vh; left: 0"
    @click="closeModal"
  ></section>
  <section
    v-if="bool"
    class="position-absolute d-flex justify-content-center align-items-start p-2"
    style="
      z-index: 80;

      left: 50%;
      top: 50%;
      transform: translate(-50%, -50%);
      height: 100vh;
      margin-top: 20vh;
    "
  >
    <form
      class="mt-10 d-flex flex-column border border-dark p-2 border-3 h-50 position-fixed"
      @submit.prevent="editTask"
    >
      <input
        class="border rounded p-2 mb-2"
        v-model.lazy="newTask.title"
        placeholder="Title"
        type="text"
        @focus="focus"
      />
      <textarea
        @focus="focus"
        ref="texsearch"
        rows="20"
        class="border rounded p-2 mb-2"
        v-model.lazy="newTask.description"
        placeholder="Task Details"
        type="text"
      ></textarea>
      <button
        class="border rounded p-2 bg-success text-white"
        @submit.prevent=""
      >
        Edit Task
      </button>
    </form>
  </section>
</template>

<script>
export default {
  inheritAttrs: false,
  taskers: "",
  name: "EditTask",
  props: ["showVal", "bool"],
  data() {
    return {
      focuss: false,
      showValue: "aa",
      newTask: {
        title: "",
        description: "",
      },
    };
  },
  methods: {
    //try to load the task in to input value before update
    // test() {
    //         if (this.focuss) {
    //             console.log("aa");
    //             this.newTask.title = "";
    //             this.newTask.description = "";
    //         }
    //         else {
    //         }
    // },
    focus() {
      this.focuss = true;
      console.log(this.focuss);
    },
    closeModal() {
      this.$emit("set-bool", false);
    },
    showModal() {
      this.$emit("set-bool", true);
      // auto focus
      this.$nextTick(() => {
        this.$refs.textsearch.focus();
      });
    },
    editTask() {
      this.showValue = this.showVal;
      this.emitter.emit("edit-task-new", {
        newTask: this.newTask,
        index: this.showValue.index,
      });
      this.$emit("set-bool", false);
    },
  },

  // beforeUpdate() {
  //     this.test();
  // },
};
</script>
<style></style>
