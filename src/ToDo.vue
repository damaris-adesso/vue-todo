<script setup lang="ts">
import { ref } from "vue";
import ToDoItem from "./components/ToDoItem.vue";

const list = ref([
  { todo: "clean the house", id: 1 },
  { todo: "buy milk", id: 2 },
]);
const todo = ref("");

function generateId() {
  if (list.value && list.value.length) {
    return Math.max(...list.value.map((t) => t.id)) + 1;
  } else {
    return 1;
  }
}

function updateList() {
  if (!todo.value || todo.value === "") {
    return;
  }
  const newId = generateId();
  list.value = [...list.value, { todo: todo.value, id: newId }];
  // alternative
  // list.value.push({todo: todo.value})
  todo.value = "";
}

function deleteFromList(id: number) {
  list.value = list.value.filter((item) => item.id !== id);
}
</script>

<template>
  <div class="ToDo">
    <div class="ToDo-Container">
      <header>
        <img alt="Vue logo" class="logo" src="./assets/logo.svg" />
        <h2 class="Headline">Vue To Do</h2>
      </header>

      <ul>
        <ToDoItem
          v-for="todo of list"
          :key="todo.id"
          :todo="todo"
          :removeItem="deleteFromList"
        />
      </ul>
      <input
        type="text"
        v-model="todo"
        v-on:keyup.enter="updateList"
        placeholder="I need to ..."
      />
      <button class="ToDo-Add" @click="updateList">+</button>
    </div>
  </div>
</template>

<style scoped>
.ToDo {
  text-align: center;
  border: 1px solid white;
  border-radius: 15px;
  width: 80vw;
  height: auto;
  box-shadow: 2px 3px 15px rgba(0, 0, 0, 0.5);
  background: #f6f6f6;
  padding-bottom: 60px;
  margin: 40px auto;
}

.ToDo-Container {
  width: 80%;
  margin: 0 auto;
}

.logo {
  width: 70px;
  margin-top: 50px;
}

.Headline {
  text-transform: uppercase;
  font-weight: 400;
}

input {
  width: 60%;
  padding: 10px;
  font-size: 1em;
  margin: 10px auto;
  box-shadow: 1px 3px 20px 0px rgba(0, 0, 0, 0.3);
  border-radius: 10px;
}

.ToDo-Add {
  color: white;
  font-size: 2em;
  width: 40px;
  height: 40px;
  padding: 0px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  background: #258c5d;
  border-radius: 10px;
  box-shadow: 1px 1px 1px #258c5d;
  margin: 20px auto 0;
}

.ToDoItem {
  display: flex;
  justify-content: center;
  align-items: center;
}

.ToDoItem-Text {
  width: 90%;
  background-color: white;
  border: 1px solid lightgrey;
  border-radius: 10px;
  box-shadow: 1px 1px 1px lightgrey;
  padding: 12px;
  margin-right: 10px;
}

.ToDoItem-Delete {
  width: 35px;
  /*padding: 5px;*/
  height: 35px;
  cursor: pointer;
  background: #ff6900;
  border-radius: 10px;
  box-shadow: 1px 1px 1px #ff6900;
  color: white;
  font-size: 18px;
  margin-right: 5px;
}

.ToDoItem-Delete:hover {
  box-shadow: none;
  margin-top: 1px;
  margin-left: 1px;
}
</style>
