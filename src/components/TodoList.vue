<template>
  <div>
    <h1>Todo List</h1>
    <input
      v-model="newTask"
      v-on:keyup.enter="addTask"
      placeholder="Add new task"
    />
    <ul>
      <li v-for="(task, index) in tasks" :key="index">
        <input type="checkbox" v-model="task.completed" />
        <span v-bind:class="{ completed: task.completed }">{{
          task.text
        }}</span>
        <button v-on:click="removeTask(index)">Удалить</button>
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
import { ref, reactive, watch } from "vue"

const newTask = ref("")
const tasks = reactive<{ text: string; completed: boolean }[]>([])

const addTask = () => {
  if (newTask.value.trim()) {
    tasks.push({ text: newTask.value, completed: false })
    newTask.value = ""
  }
}

const removeTask = (index: number) => {
  tasks.splice(index, 1)
}

watch(tasks, (newTasks) => {
  console.log("Tasks updated:", newTasks)
})
</script>

<style scoped>
.completed {
  text-decoration: line-through;
}
</style>
