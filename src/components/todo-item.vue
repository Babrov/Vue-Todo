<script setup>
defineProps([
  'item', 'remove', 'done', 'undo'
])
</script>


<template>
  <div class="item" :class="{done: item.done}">
    <div class="buttons">
      <button @click="done(item.id)" v-if="!item.done">Done</button>
      <button @click="undo(item.id)" v-if="item.done">Undo</button>
      <button @click="remove(item.id)">Delete</button>
    </div>
    <p>{{ item.text }}</p>
  </div>
</template>

<style scoped>
.item {
  border: 1px solid white;
  border-radius: 15px;
  padding: 20px 10px;
  color: white;
}

.done {
  border-color: green;
  text-decoration: line-through;
}

@media (min-width: 1024px) {
}
</style>