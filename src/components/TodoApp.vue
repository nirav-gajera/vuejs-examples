<script setup>
import { ref, computed } from 'vue';

const task = ref('');
const editedTask = ref(null);
const statuses = ref(['to-do', 'in-progress', 'finished']);

const tasks = ref([
  {
    name: 'Learn VueJs.',
    status: 'to-do',
  },
  {
    name: 'create personal blog in laravel.',
    status: 'in-progress',
  },
  {
    name: 'learn php and laravel',
    status: 'finished',
  },
]);

const capitalizeFirstChar = (str) => {
  return str.charAt(0).toUpperCase() + str.slice(1);
};

const changeStatus = (index) => {
  let newIndex = statuses.value.indexOf(tasks.value[index].status);
  if (++newIndex > 2) newIndex = 0;
  tasks.value[index].status = statuses.value[newIndex];
};

const deleteTask = (index) => {
  tasks.value.splice(index, 1);
};

const editTask = (index) => {
  task.value = tasks.value[index].name;
  editedTask.value = index;
};

const submitTask = () => {
  if (task.value.length === 0) return;

  if (editedTask.value !== null) {
    tasks.value[editedTask.value].name = task.value;
    editedTask.value = null;
  } else {
    tasks.value.push({
      name: task.value,
      status: 'todo', 
    });
  }

  task.value = '';
};

const characterCount = computed(() => {
  return task.value.length;
});
</script>

<template>
    <div class="container" style="max-width: 600px">
      <h2 class="text-center mt-5">My Vue Todo App</h2>
  
      <div class="d-flex mt-5">
        <input
          type="text"
          v-model="task"
          placeholder="Enter task"
          class="w-100 form-control"
        />
        <button class="btn btn-success" @click="submitTask">
          Submit
        </button>
     
      </div>
      <p class="counter">
        {{ characterCount }}/100
        </p>
  
      <table class="table table-bordered mt-5">
        <thead>
          <tr>
            <th scope="col">Task</th>
            <th scope="col" style="width: 120px">Status</th>
            <th scope="col" class="text-center">Delete</th>
            <th scope="col" class="text-center">Edit</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(task, index) in tasks" :key="index">
            <td>
              <span :class="{ 'line-through': task.status === 'finished' }">
                {{ task.name }}
              </span>
            </td>
            <td>
              <span
                class="pointer noselect"
                @click="changeStatus(index)"
                :class="{
                  'text-danger': task.status === 'to-do',
                  'text-success': task.status === 'finished',
                  'text-warning': task.status === 'in-progress',
                }"
              >
                {{ capitalizeFirstChar(task.status) }}
              </span>
            </td>
            <td class="text-center">
              <div @click="deleteTask(index)">
                <span class="fa fa-trash pointer"></span>
              </div>
            </td>
            <td class="text-center">
              <div @click="editTask(index)">
                <p class="fa fa-pen pointer"></p>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  export default {
    name: "HelloWorld",
    props: {
      msg: String,
    },
  };
  </script>
  
  
  <style scoped>
  .pointer {
    cursor: pointer;
  }
  .noselect {
    -webkit-touch-callout: none;
    -webkit-user-select: none; 
    -khtml-user-select: none; 
    -moz-user-select: none; 
    -ms-user-select: none; 
    user-select: none; 
  }
  .line-through {
    text-decoration: line-through;
  }
  </style>
  <script setup>
  
  </script>