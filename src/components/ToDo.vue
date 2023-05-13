<template>
  <section class="h-75 border border-dark border-3 w-100 m-2 overflow-scroll">
    <slot></slot>
  </section>
</template>

<script>

export default {
  components: {
    //Tasks,
  },
  editTask:"",
  name: "ToDo",
  props: ["tasker"],
};

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
</style>
