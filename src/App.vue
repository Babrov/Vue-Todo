<script setup>
import {ref} from "vue";
import ItemList from "@/components/item-list.vue";

const id = ref(6);

const todoItems = ref([
  {id: 2, text: 'Learn about single file components', done: false},
  {id: 3, text: 'Fall in love', done: false},
])
const doneItems = ref([
  {id: 1, text: 'Learn Vue', done: true},
  {id: 4, text: 'Learn about the composition API', done: true},
  {id: 5, text: 'Learn about the options API', done: true},
])
const newItem = ref({
  text: '',
  done: false
})

const addNew = () => {
  (newItem.value.done ? doneItems : todoItems).value.push({...newItem.value, id: id.value++})
}
const removeDoneItem = (removeId) => {
  doneItems.value = doneItems.value.filter(item => item.id !== removeId);
}
const removeToDoItem = (removeId) => {
  todoItems.value = todoItems.value.filter(item => item.id !== removeId);
}
const done = (id) => {
  const item = todoItems.value.find(item => item.id === id);
  item.done = true;
  doneItems.value.push(item);
  removeToDoItem(id);
}

const undo = (id) => {
  const item = doneItems.value.find(item => item.id === id);
  item.done = false;
  todoItems.value.push(item);
  removeDoneItem(id);
}

</script>

<template>
  <header>
    <h1>Vue TODO App</h1>
  </header>

  <div>
    <h2>Add new TODO:</h2>
    <input v-model="newItem.text" placeholder="Text"/>
    <label for="checkbox">Is Done?</label>
    <input type="checkbox" id="checkbox" v-model="newItem.done" placeholder="Is done"/>
    <button @click="addNew">Add</button>
  </div>

  <main>
    <div>
      <h2>TODO:</h2>
      <ItemList :items="todoItems" :onDone="done" :onRemove="removeToDoItem"/>
    </div>
    <div>
      <h2>DONE:</h2>
      <ItemList :items="doneItems" :onUndo="undo" :onRemove="removeDoneItem"/>
    </div>
  </main>
</template>

<style scoped>
main {
  display: flex;
  justify-content: space-around;
  flex-direction: column;
}

@media (min-width: 1024px) {
  main {
    flex-direction: row;
  }
}
</style>
