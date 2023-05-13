<template>
<div class="dropdown">
    <button
      class="btn btn-secondary dropdown-toggle h-75"
      type="button"
      id="dropdownMenuButton1"
      data-bs-toggle="dropdown"
      aria-expanded="false"
    >
      {{ value }}
    </button>
    <ul class="dropdown-menu" aria-labelledby="dropdownMenuButton1" role="menu">
      <li v-for="option in options" :key="option">
        <a
          class="dropdown-item"
          @click="(value = option);runder;rundet;setBool;test;runTest"
          href="javascript:void(0)"
          >{{ option }}</a
        >
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Dropdown",
  data() {
    return {
      options: ["Edit", "Delete"],
      value: "",
    };
  },
  computed:{
    runder(){
     return this.$emit("edit-task", this.value) 

    },
    test(){
      return this.$emit("edit-task-test")
    },
    rundet(){
      return this.$emit("edit-task-index",this.value)
    }, 
    setBool(){
      return this.$emit("set-bool")
    },
    runTest(){
     return this.emitter.emit("run-test",true)
    },
  }
};
</script>


<style>
</style>