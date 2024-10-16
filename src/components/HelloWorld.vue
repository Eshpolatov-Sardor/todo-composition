<script setup lang="ts">
import { ref } from "vue";
let text = ref("");
let text1 = ref("");
let ListTodo = ref([
  {
    text: "Sardor" as string,
    text1: "QDPU" as string,
    active: false as boolean
  },
  {
    text: "Asilbek" as string,
    text1: "TATU" as string,
    active: false as boolean
  },
  {
    text: "Eshpo'latov" as string,
    text1: "TATU" as string,
    active: false as boolean
  }
]);
let showModal = ref(false);

function submit() {
  if(text.value!=="" && text1.value!==""){
    const addListTodo = {
    text: text.value as string,
    text1: text1.value as string,
    active : false as boolean
  };
  ListTodo.value.push(addListTodo);
  }
  else{
    alert("inputlarni tuldirmadingiz")
  }
  (text.value = ""), (text1.value = ""), closeModal();

  localStorage.setItem('todos',JSON.stringify(ListTodo.value))
}

  function clearTodo(index:number){
    ListTodo.value.splice(index,1)
    localStorage.setItem("todos", JSON.stringify(ListTodo.value));
  }

function AddTodo() {
  showModal.value = true;
}
function closeModal() {
  showModal.value = false;
}
function toggleActive(index: number) {
  ListTodo.value[index].active = !ListTodo.value[index].active;
}
</script>
<template>
  <div class="flex justify-center items-center flex-col mt-5">
    <h1
      @click="AddTodo"
      class="rounded-full border border-black bg-blue-600 w-32 h-10 flex justify-center items-center cursor-pointer"
    >
      Add Todo
    </h1>

    <div
      v-if="showModal"
      class="fixed inset-0 flex justify-center items-center bg-black bg-opacity-50"
    >
      <div class="bg-white p-5 rounded shadow-lg">
        <form @submit.prevent="submit">
          <label for="text" class="block font-semibold mb-2">Title:</label>
          <input
            type="text"
            v-model="text"
            class="border p-2 w-full rounded mb-4"
            placeholder="Enter Title"
          />

          <label for="text1" class="block font-semibold mb-2"
            >Description:</label
          >
          <input
            type="text"
            v-model="text1"
            class="border p-2 w-full rounded mb-4"
            placeholder="Enter Description"
          />

          <div class="flex justify-end space-x-2">
            <button
              type="submit"
              class="bg-blue-600 text-white px-4 py-2 rounded"
            >
              Add
            </button>
            <button
              type="button"
              @click="closeModal"
              class="bg-gray-300 px-4 py-2 rounded"
            >
              Close
            </button>
          </div>
        </form>
      </div>
    </div>
    <ol>
      <li
        v-for="(item, index) in ListTodo"
        :key="index"
        class="flex w-64 justify-between items-center mt-5 p-2 border border-black rounded-lg"
        :class="{ 'line-through': item.active }"
      >
        <span>
          <p>{{ item.text }}</p>
          <p>{{ item.text1 }}</p>
        </span>
        <span class="flex items-center gap-2">
          <input class="w-3 h-3 border border-black cursor-pointer" type="checkbox" :checked="item.active" @change="toggleActive(index)">
          <button @click="clearTodo(index)"><svg data-v-ce1a3ef4 width="22" height="22" viewBox="0 0 22 22" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M1 5H21M9 10V15M13 10V15M3 5H19L17.42 19.22C17.3658 19.7094 17.1331 20.1616 16.7663 20.49C16.3994 20.8184 15.9244 21 15.432 21H6.568C6.07564 21 5.60056 20.8184 5.23375 20.49C4.86693 20.1616 4.63416 19.7094 4.58 19.22L3 5ZM6.345 2.147C6.50675 1.80397 6.76271 1.514 7.083 1.31091C7.4033 1.10782 7.77474 0.999996 8.154 1H13.846C14.2254 0.999806 14.5971 1.10755 14.9176 1.31064C15.2381 1.51374 15.4942 1.80381 15.656 2.147L17 5H5L6.345 2.147V2.147Z" stroke="#FF4545" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"></path>
          </svg></button>
        </span>
      </li>
    </ol>
  </div>
</template>
<style scoped>
</style>
