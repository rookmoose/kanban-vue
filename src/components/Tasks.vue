<template>
  <div>
    <Task
      class="mt-2"
      :tasker="tasker"
      :Progress="Progress"
      :Completed="Completed"
      @send-delete="del"
    />
  </div>
</template>

<script>
import Task from "@/components/Task.vue"

export default {
	name:'Tasks',
	editTask:"",
	components:{
		Task,
	},
	props:['tasker','Progress','Completed'],
}
</script>

<style></style>
