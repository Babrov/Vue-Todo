<script setup>
import TodoItem from "@/components/todo-item.vue";

defineProps(['items', 'onRemove', 'onDone', 'onUndo'])
</script>

<template>
  <div class="items">
    <TodoItem :done="onDone" :undo="onUndo" :remove="onRemove" v-for="item in items" :key="item.id"
              :item="item"/>
  </div>
</template>