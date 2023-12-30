<script setup lang="ts">
import type { Column } from "~/types";
import { nanoid } from "nanoid";
import draggable from "vuedraggable";
const columns = ref<Column[]>([
  {
    id: nanoid(),
    title: "Backlog",
    tasks: [
      {
        id: nanoid(),
        title: "Create marketing landing page",
        createdAt: new Date()
      },
      {
        id: nanoid(),
        title: "Fix page nav bug",
        createdAt: new Date()
      },
      {
        id: nanoid(),
        title: "Develop new feature",
        createdAt: new Date()
      },
    ]
  },
  {
    id: nanoid(),
    title: "Selected for next sprint",
    tasks: []
  },
  {
    id: nanoid(),
    title: "In progress",
    tasks: []
  },
  {
    id: nanoid(),
    title: "QA",
    tasks: []
  }
])
</script>
<template>
  <div class="flex gap-4 overflow-x-auto items-start">
    <div
      v-for="column in columns"
      :key="column.id"
      class="bg-gray-200 rounded p-5 min-w-[250px]"
    >
      <header class="font-bold mb-4">{{ column.title }}</header>
      <TrelloBoardTask v-for="task in column.tasks" :task="task" :key="task.id"/>
      <footer>
        <button class="text-gray-500">+ Add a card</button>
      </footer>
    </div>
  </div>
</template>
