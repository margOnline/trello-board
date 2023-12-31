<script setup lang="ts">
import type { Column } from "~/types";
import { nanoid } from "nanoid";
import Draggable from "vue3-draggable";
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
  },
  {
    id: nanoid(),
    title: "Complete",
    tasks: []
  }
])
</script>
<template>
  <div>
    <draggable
      v-model="columns"
      group="columns"
      item-key="id"
      :transition="'150'"
      handle=".drag-handle"
      class="flex gap-4 overflow-x-auto items-start"
    >
      <template v-slot:item="{item: column}:{item: Column}">
        <div class="bg-gray-200 rounded p-5 min-w-[250px]">
          <header class="font-bold mb-4">
            <DragHandle />
            {{ column.title }}
          </header>
          <TrelloBoardTask v-for="task in column.tasks" :task="task" :key="task.id"/>
          <footer>
            <button class="text-gray-500">+ Add a card</button>
          </footer>
        </div>
      </template>
    </draggable>
  </div>
</template>
