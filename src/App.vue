<script setup lang="ts">
import { computed, ref } from "vue";
import Card from "./components/Card.vue";
import { nanoid } from "nanoid";
import AddTodoForm from "./components/AddTodoForm.vue";

type Todos = {
  value: string;
  completed: boolean;
  id: string;
};

let inputValue = ref("");

let todos = ref<Todos[]>([]);

let storedTodo = localStorage.getItem("todos");

if (storedTodo) {
  todos.value = JSON.parse(storedTodo) as Todos[];
}

const addTodoList = (todoValue: string) => {
  todos.value.push({ value: todoValue, completed: false, id: nanoid() });
  localStorage.setItem("todos", JSON.stringify(todos.value));
  inputValue.value = "";
};

const deleteTodoList = (id: string) => {
  todos.value = todos.value.filter((todo) => todo.id !== id);
  localStorage.setItem("todos", JSON.stringify(todos.value));
};

const updateTodoItem = (todoValue: string) => {
  // alert(todoValue);
  // const index = todos.value.findIndex((item) => item.id === id);
  inputValue.value = todoValue;
  // todos.value[index].value = todoValue;
};

const reversedTodoList = computed(() => [...todos.value].reverse());
</script>

<template>
  <div
    class="flex w-full min-h-screen flex-col gap-5 py-0 md:py-10 items-center justify-start bg-slate-100 text-black"
  >
    <div
      class="md:h-1/5 hidden md:flex absolute bg-gradient-to-tl from-slate-900 to-slate-500 shadow-sm w-full top-0"
    ></div>
    <AddTodoForm :inputValue="inputValue" @addTodoList="addTodoList" />

    <div
      class="flex flex-col gap-3 w-full min-h-screen md:w-2/3 lg:w-1/2 rounded-md shadow-lg p-5 bg-white"
    >
      <h1 class="text-black text-xl font-bold text-left">Todo Lists</h1>
      <!-- <h1>{{ inputValue }}</h1> -->
      <Card
        v-for="todo of reversedTodoList"
        :todo="todo"
        @deleteTodoList="deleteTodoList"
        @updateTodoItem="updateTodoItem"
      />
      <div v-if="todos?.length == 0">
        <p class="text-center text-lg">No todo list yet.</p>
      </div>
    </div>
  </div>
</template>
