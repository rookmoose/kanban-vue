<template>
  <section class="d-flex flex-column">
    <div class="p-2 d-flex justify-content-around" style="height: 100vh">
      <draggable
        :tasker="tasker"
        animation="600"
        @start="drag = true"
        @end="drag = false"
        class="d-flex justify-content-around p-2 w-100 h-100"
      >
        <to-do
          :tasker="tasker"
          @edit-task-new="addTask"
          @test-focus="clear"
          @send-delete="del"
        >
          <h3 class="w-[50vw] bg-secondary mb-2 rounded fs-4 p-2 text-white">
            To Do
          </h3>
            <Tasks :tasker="tasker" />
        </to-do>

        <to-do
          @edit-task-new="addTask"
          @test-focus="clear"
          @send-delete="del"
          :tasker="tasker"
        >
          <h3 class="w-100 bg-warning mb-2 rounded fs-4 p-2 text-white">
            In Progress
          </h3>
          <Tasks :Progress="Progress" />
        </to-do>

        <to-do
          @edit-task-new="addTask"
          @test-focus="clear"
          @send-delete="del"
          :tasker="tasker"
        >
          <h3 class="w-100 bg-primary mb-2 rounded fs-4 p-2 text-white">
            Completed
          </h3>
          <Tasks :Completed="Completed" />
        </to-do>
        <CreateTask
          @send-delete="del"
          @new-task="addTasktoTasks"
          :tasker="tasker"
          class="border rounded"
          :isModal="modalOpen"
        />
      </draggable>
    </div>
  </section>
</template>

<script>
// @ is an alias to /src
import ToDo from "@/components/ToDo.vue";
import CreateTask from "@/components/CreateTask.vue";
import Tasks from "@/components/Tasks.vue";
import { VueDraggableNext } from "vue-draggable-next";

export default {
  name: "Home",

  components: {
    ToDo,
    CreateTask,
    Tasks,
    draggable: VueDraggableNext,
  },
  data() {
    return {
      focus: false,
      tasker: [],
      Progress: [],
      Completed: [],
      drag: false,
    };
  },
  methods: {
    addTasktoTasks(value) {
      this.tasker.push(value);
    },

    addTask() {
      this.emitter.on("edit-task-new", (val) => {
        console.log(val.newTask);
        this.tasker[val.index] = val.newTask;
      });
    },
    del() {
      this.emitter.on("send-delete", (val) => {
        this.tasker.splice(val.index, 1);
      });
    },
  },
  mounted() {
    this.addTask();
    this.del();
  },
};
</script>
