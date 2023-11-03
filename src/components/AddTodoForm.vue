<script setup lang="ts">
import { ref, defineModel } from "vue";

defineProps<{ addTodoList?: any }>();
// const parentInputValue = defineModel<string>("inputValue");
const emit = defineEmits(["addTodoList"]);
const inputValue = ref("");

console.log("parentInputValue", inputValue);

const handleAddTodo = () => {
  // alert(inputValue);
  if (inputValue.value) {
    emit("addTodoList", inputValue.value);
    inputValue.value = "";
  }
};

// const handleUpdateTodoItem = () => {
//   emit("addTodoList");
// };
</script>

<template>
  <form
    class="md:w-2/3 lg:w-1/2 w-full h-fit bg-white px-10 py-10 md:py-9 rounded-md shadow-lg items-center justify-start flex flex-col gap-5 z-50"
    @submit="handleAddTodo"
  >
    <h1 class="text-black text-3xl font-bold text-center">Todo List</h1>
    <div class="w-full flex bg-slate-200 shadow-sm rounded-lg">
      <input
        type="text"
        placeholder="What would you like to do?"
        v-model="inputValue"
        :required="true"
        class="bg-slate-200 font-medium text-lg border-none focus:ring-[1px] shadow-sm outline-none rounded-l-xl md:py-3 px-6 w-full"
      />
      <button
        class="bg-green-600 font-bold uppercase px-5 md:px-14 py-2 text-lg rounded-r-lg shadow-md text-white disabled:bg-slate-600 disabled:cursor-not-allowed"
        :disabled="inputValue.length == 0"
      >
        Add
      </button>
    </div>
  </form>
</template>
