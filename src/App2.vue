<script>
//option api
export default{
  data(){
    return{
      name:'John Doe',
      status:'active',
      tasks:['Task 1','Task 2','Task 3'],
      link:'https://google.com',
    };
  },
  methods:{
    toggleStatus(){
      this.status = this.status === 'active' ? 'pending' : 'active';
    }
  }
}
</script>

<template>
  <h1>Hello {{name}}</h1>
  <p v-if="status === 'active'">User Is Active</p>
  <p v-else-if="status === 'pending'">User Is Not Active</p>
  <p v-else>User Is Unknown</p>
  <h3>Tasks:</h3>
  <ul>
    <li v-for="task in tasks" :key="task">{{ task }}</li>
  </ul>
  <a v-bind:href="link">1.Click For Google</a>
  <a :href="link">2.Click For Google</a>
  <br>
  <button v-on:click="toggleStatus">Change Status1</button>
  <button @click="toggleStatus">Change Status2</button>
</template>
//yeni
<script>
import { onMounted, ref } from 'vue';

export default {
  setup() {
    const name = ref('John Doe');
    const status = ref('active');
    const tasks = ref(['Task 1', 'Task 2', 'Task 3']);
    const newTask = ref('');
    const link = ref('https://www.google.com'); // Added the missing link variable

    const toggleStatus = () => {
      status.value = status.value === 'active' ? 'pending' : 'active';
    };

    const addTask = () => {
      if (newTask.value.trim() !== '') {
        tasks.value.push(newTask.value);
        newTask.value = '';
      }
    };
    const deleteTask = (index) => {
      tasks.value.splice(index, 1);
    };
    onMounted(async () => {
      try {
        const response = await fetch('https://jsonplaceholder.typicode.com/todos');
        const data = await response.json();
        tasks.value = data.map((task) => task.title);
      } catch (error) {
        console.log("error fetching tasks");
      }
    })

    return {
      name,
      status,
      tasks,
      newTask,
      link,
      toggleStatus,
      addTask,
      deleteTask,
    };
  },
};
</script>

<template>
  <h1>Hello {{ name }}</h1>
  <p v-if="status === 'active'">User Is Active</p>
  <p v-else-if="status === 'pending'">User Is Not Active</p>
  <p v-else>User Is Unknown</p>

  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text" name="newTask" id="newTask" v-model="newTask" />
    <button type="submit">Submit</button>
  </form>

  <h3>Tasks:</h3>
  <ul>
    <li v-for="(task,index) in tasks" :key="task">
      <span>{{ task }}</span>
      <button @click="deleteTask(index)">x</button>
    </li>
  </ul>

  <a :href="link">1. Click For Google</a>
  <a :href="link">2. Click For Google</a>
  <br />

  <button @click="toggleStatus">Change Status1</button>
  <button @click="toggleStatus">Change Status2</button>
</template>


