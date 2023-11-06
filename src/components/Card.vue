<script setup lang="ts">
// defineProps<{ msg: string }>();

defineProps<{
  todo: {
    value: string;
    completed: boolean;
    id: string;
  };
  inputValue: string;
  todoId: string;
}>();

const emit = defineEmits([
  "deleteTodoList",
  "update:inputValue",
  "update:todoId",
]);
const handleDeleteTodoItem = (id: string | undefined) => {
  emit("deleteTodoList", id);
};
const handleUpdateTodoItem = (value: string, id: string) => {
  emit("update:inputValue", value);
  emit("update:todoId", id);
};
</script>

<template>
  <div
    class="bg-white flex border-2 rounded-lg shadow-md px-6 py-3 items-center justify-center gap-2"
  >
    <input
      type="checkbox"
      value="completed"
      class="bg-white fill-white accent-green-700 w-7 h-4 border-none"
      v-model="todo.completed"
      :checked="todo.completed"
    />
    <h1
      class="text-lg font-medium mr-auto"
      :class="{
        'line-through': todo.completed,
        'text-gray-400': todo.completed,
      }"
    >
      {{ todo.value }}
    </h1>
    <svg
      xmlns="http://www.w3.org/2000/svg"
      class="w-5 h-5 fill-amber-600 mr-1"
      viewBox="0 0 24 24"
      @click="handleUpdateTodoItem(todo.value, todo.id)"
    >
      <path
        d="M5 18.89H6.41421L15.7279 9.57629L14.3137 8.16207L5 17.4758V18.89ZM21 20.89H3V16.6474L16.435 3.21233C16.8256 2.8218 17.4587 2.8218 17.8492 3.21233L20.6777 6.04075C21.0682 6.43128 21.0682 7.06444 20.6777 7.45497L9.24264 18.89H21V20.89ZM15.7279 6.74786L17.1421 8.16207L18.5563 6.74786L17.1421 5.33365L15.7279 6.74786Z"
      ></path>
    </svg>
    <svg
      xmlns="http://www.w3.org/2000/svg"
      class="w-5 h-5 fill-red-500"
      viewBox="0 0 24 24"
      @click="handleDeleteTodoItem(todo.id)"
    >
      <path
        d="M4 8H20V21C20 21.5523 19.5523 22 19 22H5C4.44772 22 4 21.5523 4 21V8ZM6 10V20H18V10H6ZM9 12H11V18H9V12ZM13 12H15V18H13V12ZM7 5V3C7 2.44772 7.44772 2 8 2H16C16.5523 2 17 2.44772 17 3V5H22V7H2V5H7ZM9 4V5H15V4H9Z"
      ></path>
    </svg>
  </div>
</template>
