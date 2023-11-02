<script setup lang="ts">
import { ref } from "vue";
import Card from "./components/Card.vue";

type Todos = string;

let inputValue = ref("");

const todos = ref<Todos[]>([]);

const addTodoList = (todoValue: Todos) => {
  todos.value.push(todoValue);
  inputValue.value = "";
};
</script>

<template>
  <div
    class="flex w-full h-screen justify-center gap-5 items-center bg-slate-900 text-black"
  >
    <div
      class="w-1/2 h-1/2 bg-white px-10 py-5 rounded-md shadow-lg flex flex-col gap-5"
    >
      <h1 class="text-black text-3xl font-bold">Todo Lists</h1>
      <div class="w-full flex bg-slate-200 shadow-sm rounded-xl">
        <input
          type="text"
          placeholder="Enter your todo list here"
          v-model="inputValue"
          class="bg-slate-200 font-medium text-lg rounded-l-xl p-5 w-full"
        />
        <button
          class="bg-green-600 font-bold uppercase px-16 py-2 text-lg rounded-xl shadow-md text-white"
          @click="addTodoList(inputValue)"
        >
          Add
        </button>
      </div>
      <div
        class="flex flex-col gap-3 h-full rounded-md shadow-sm p-5 bg-slate-100"
      >
        <Card v-for="todo of todos" :todo="todo" />
      </div>
    </div>
  </div>
</template>
