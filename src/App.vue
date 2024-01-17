<script setup>
import { ref } from 'vue';
const tasks = ref([{
  name: 'Task 1',
  time: 30
}, {
  name: 'Task 2',
  time: 40
}, {
  name: 'Task 3',
  time: 60
}, {
  name: 'Task 4',
  time: 45
}, {
  name: 'Task 5',
  time: 50
}]);


const taskIndex = ref();
const taskData = {
  name: '',
  time: ''
}
const popUp = ref(false);
function taskEdit(dataIndex){
    popUp.value = true;
    taskData.name = tasks.value[dataIndex].name;
    taskData.time = tasks.value[dataIndex].time;
    taskIndex.value = dataIndex;
}
function popupClose(){
  popUp.value = false;
}
function updateIndex(updatedIndex){
  taskIndex.value = updatedIndex.value;
}
function updateTask(){
  tasks.value[taskIndex.value].name = taskData.name;
  tasks.value[taskIndex.value].time = taskData.time;
  popUp.value = false;
}
</script>

<template>
  <!-- ======Popup Start======= -->
  <div v-show="popUp" class="relative z-10" aria-labelledby="modal-title" role="dialog" aria-modal="true">
        <div class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity"></div>

        <div class="fixed inset-0 z-10 w-screen overflow-y-auto">
            <div class="flex min-h-full items-end justify-center p-4 text-center sm:items-center sm:p-0">

                <div class="relative transform overflow-hidden rounded-lg bg-white text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg">
                    <form @submit.prevent="updateTask" class="w-full">
                    <div class="bg-white px-4 pb-4 pt-5 sm:p-6 sm:pb-4">
                        <div class="sm:flex sm:items-start">
                            <div class="mx-auto flex h-12 w-12 flex-shrink-0 items-center justify-center rounded-full bg-green-100 sm:mx-0 sm:h-10 sm:w-10">
                                <i class="fa-solid fa-list-check"></i>
                            </div>
                            <div class="mt-3 text-center sm:ml-4 sm:mt-0 sm:text-left w-5/6">
                                <h3 class="text-base font-semibold leading-6 text-gray-900" id="modal-title">Edit Task</h3>
                                
                                    <div class="sm:col-span-4 mt-3 w-full">
                                        <label for="name" class="block text-sm font-medium leading-6 text-gray-900">Task name</label>
                                        <div class="mt-2">
                                            <input v-model="taskData.name" id="name" name="name" type="text" placeholder="e.g. Task 1" class="block w-full rounded-md border-0 p-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6">
                                           
                                        </div>
                                    </div>
                                    <div class="sm:col-span-4 w-full mt-3">
                                        <label for="time" class="block text-sm font-medium leading-6 text-gray-900">Task time</label>
                                        <div class="mt-2">
                                            <input v-model="taskData.time" id="time" name="time" type="number" class="block w-full rounded-md border-0 px-1.5 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6" placeholder="e.g. 60">
                                            
                                        </div>
                                    </div>
                            </div>
                        </div>
                    </div>
                    <div class="bg-gray-50 px-4 py-3 sm:flex sm:flex-row-reverse sm:px-6">
                        <button type="submit" class="inline-flex w-full justify-center rounded-md bg-blue-500 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-blue-700 sm:ml-3 sm:w-auto">Update Task</button>
                        <button @click="popupClose" type="button" class="mt-3 inline-flex w-full justify-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50 sm:mt-0 sm:w-auto">Cancel</button>
  
                    </div>
                </form>
                </div>
            </div>
        </div>
    </div>
    <!-- ======PopUp End======= -->
  <section class="p-10 bg-green-200 w-3/5 m-auto rounded-md">
    <div class="flex flex-col">
      <h1 class="text-3xl font-semibold">Vue.js Edit Task List</h1>
      <h2 class="mt-2 text-lg font-semibold">Live Test 1</h2>
      <div class="w-96 m-auto mt-8 flex flex-col items-start">
        <div class="flex flex-col mt-2 w-full gap-2">
          <div v-show="tasks.length>0" v-for="(task, index) in tasks" :key="index" class="flex justify-between bg-slate-50 p-3 rounded-md w-full">
            <h3 class="font-medium"><span>{{ index + 1 }}. </span>{{ task.name }}</h3>
            <span class="font-medium">{{ task.time }} Min</span>
            <span class="ml-2 text-blue-500 cursor-pointer" @click="taskEdit(index)"><i class="fa-solid fa-pen-to-square"></i></span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>

</style>
