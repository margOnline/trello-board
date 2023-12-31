<script setup lang="ts">
import type { Task } from "~/types"
defineProps<{
  task: Task;
}>();
</script>

<template>
  <div
    :title="task.createdAt.toLocaleDateString()"
    class="bg-white rounded p-2 mb-2 max-w-[250px] flex"
  >
    <DragHandle class="pr-2" />
    <span>{{ task.title }}</span>
  </div>
</template>