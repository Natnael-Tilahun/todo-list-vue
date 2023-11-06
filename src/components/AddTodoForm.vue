<script setup lang="ts">
import { Ref, onMounted, ref } from "vue";

// defineProps<{inputValue: string }>();
const props = defineProps({
  inputValue: String,
});
const emit = defineEmits(["update:inputValue", "addTodoList"]);
const TodoMaxValue: number = 50;

const todoInput: Ref<HTMLInputElement | null> = ref(null);

const handleAddTodo = () => {
  emit("addTodoList", props.inputValue);
};

onMounted(() => {
  if (todoInput.value) {
    todoInput.value.focus();
  }
});
</script>

<template>
  <form
    class="md:w-2/3 lg:w-1/2 w-full h-fit bg-white px-10 py-10 md:py-9 rounded-md shadow-lg items-center justify-start flex flex-col gap-5 z-50"
    @submit="handleAddTodo"
  >
    <h1 class="text-black text-3xl font-bold text-center">Todo List</h1>
    <div class="w-full">
      <div class="w-full flex bg-slate-200 shadow-sm rounded-lg">
        <input
          type="text"
          placeholder="What would you like to do?"
          :value="inputValue"
          @input="($event) => $emit('update:inputValue', ($event?.target as HTMLInputElement) ?.value)"
          :required="true"
          :maxlength="TodoMaxValue"
          ref="todoInput"
          class="bg-slate-200 font-medium text-lg border-none focus:ring-[1px] shadow-sm outline-none rounded-l-xl md:py-3 px-6 w-full"
        />
        <button
          class="bg-green-600 font-bold uppercase px-5 md:px-14 py-2 text-lg rounded-r-lg shadow-md text-white disabled:bg-slate-600 disabled:cursor-not-allowed"
          :disabled="props.inputValue?.length == 0"
        >
          Add
        </button>
      </div>
      <p
        class="text-left w-full text-gray-600 py-1"
        :class="
          (inputValue ?? '')?.length >= TodoMaxValue ? 'text-red-600' : ''
        "
      >
        {{ inputValue?.length }} |
        {{ TodoMaxValue }}
      </p>
    </div>
  </form>
</template>
