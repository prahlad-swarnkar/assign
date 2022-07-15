<template>
  <div>
    <!-- Logo -->
    <h1> &#128203
    <!-- Title -->
    <span> {{ title }} </span> 
    </h1>
  </div>

  <!-- Data Division -->
  <div class='main'>

    <!-- New Task Division -->
    <div class='data' style='background-color: white;'>
    <table><tr>
      <td>
      <input type='text' v-model='newTask' 
      @keyup.enter='addTask'
      placeholder='Add a new task'>
      </td>
      <td>
      <button @click='addTask' id='ad'
      :disabled='newTask.length < 1'> &#43
      </button>
      </td>
    </tr></table>
    </div>

    <!-- Task List Division -->
    <div class='data' style='padding: 2%;'>
    <table>
      <tr>
      <th>Tasks</th>
      <!-- Brief Info -->
      <td class='opt'>
        <span style='color: #0073d6;'>Total {{ allTasks }}
        </span>
        <span style='color: #d7514d;'>
          Remaining {{ remainTasks }}
        </span>
        <span style='color: #5ab65a;'>
        Completed {{ finishedTasks }}
        </span>
      </td>
      </tr>

    <!-- Task List -->
      <tr v-for='(task,index) in latest' :key='task.id'>
        <!-- Task description -->
        <td>
        <span v-if='task.finished' style='color: gray;'>
            {{ task.des }}
        </span>
        <span v-else>
            {{ task.des }}
        </span>
        </td>
        <!-- Options -->
        <td class='opt'>
          <span v-if='!task.finished'>
            <button @click='finishTask(task)'> &#10003 </button>
          </span>
          <button @click='removeTask(task.id)'> &#128465 </button>
          <button @click='editTask(task)'> &#9998 </button>
        </td>
      </tr>
    </table>

    </div>

  </div>
</template>

<script>
export default {
  data() {
    return {
      title: 'Vue ToDo',
      logoURL: 'https://images.unsplash.com/photo-1507925921958-8a62f3d1a50d?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1955&q=80',
      logoCaption: 'A photo by Kelly Sikkema on Unsplash showing post-it notes',
      tasks : [
      { id: 1, des: 'Make ToDo App', finished: true },
      { id: 2, des: 'Task @ : ???', finished: false },
      { id: 3, des: 'Guess Task 2', finished: false }
      ],
      newTask: '',
    }
  },
  methods: {
    addTask() {
      if (this.newTask.length < 1) return

        this.tasks.push({
          id: this.tasks.length + 1,
          des: this.newTask,
          finished: false
        });

      this.newTask = ''
    },
    removeTask(taskID) {
      this.tasks = this.tasks.filter(task => {
        return task.id !== taskID
      })
    },
    finishTask(t) {
      t.finished = true
    },
    editTask(t){
      this.newTask = t.des 
      this.removeTask(t.id)
    }
  },
  computed: {
    allTasks() {
      return this.tasks.length
    },
    remainTasks() {
      return this.tasks.filter(function(t){ return !t.finished; }).length
    },
    finishedTasks() {
      return this.tasks.filter(function(t){ return t.finished; }).length
    },
    latest() {
      return [...this.tasks].reverse()
    }
  }
}
</script>

<style>
.main{
  background-color: #e1ce7a;
  margin : auto;
  padding: 3%;
  border-radius: 20px;
}
.data{
  text-align: justify;
  margin : auto;
  border-radius: 10px;
}
.opt{
  text-align: right;
}
h1{
  font-size: xx-large;
  color: #c0a050;
}
table{
  width: 100%;
  font-size: medium;
  word-wrap: normal;
}
button{
  background: none;
  margin: 1%;
  border: 0px;
  font-size: larger;
  text-align: center;
  vertical-align: center;
  border-radius: 5px;
}
button:hover{
  background-color: white;
}
#ad{
  width: 100%;
  height: 100%;
  font-size: x-large;
}
#ad:hover{
  background-color: #e1ce7a;
}
input{
  margin: 1%;
  vertical-align: center;
  width: 99%;
  font-size: medium;
}
</style>
