<script setup lang="ts">
import type { Column, Task } from "~/types";
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
  },
  {
    id: nanoid(),
    title: "Complete",
    tasks: []
  }
]);
const alt = useKeyModifier("Alt");
</script>
<template>
  <div>
    <draggable
      v-model="columns"
      group="columns"
      item-key="id"
      :animation="150"
      handle=".drag-handle"
      class="flex gap-4 overflow-x-auto items-start"
    >
      <template #item="{element: column}:{element: Column}">
        <div class="column bg-gray-200 rounded p-5 min-w-[250px]">
          <header class="font-bold mb-4">
            <DragHandle />
            {{ column.title }}
          </header>
          <draggable
            v-model="column.tasks"
            :group="{name: 'tasks', pull: alt ? 'clone' : true }"
            item-key="id"
            :animation="150"
            handle=".drag-handle"
          >
            <template #item="{element: task} : {element: Task}">
              <div>
                <TrelloBoardTask :task="task" @delete="column.tasks = column.tasks.filter((t) => t.id != $event)"/>
              </div>
            </template>
          </draggable>
          <footer>
            <NewTask @add="column.tasks.push($event)" />
          </footer>
        </div>
      </template>
    </draggable>
  </div>
</template>
