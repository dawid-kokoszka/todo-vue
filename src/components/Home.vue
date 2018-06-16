<template>
  <div class="home">
      <div class="container">
      
            <h1>MyTasks <i class="fa fa-tasks" aria-hidden="true"></i></h1>
            <div class="new-task">
                <input  placeholder="Task name..." type="text" v-model="newTask">
                <button class="btn" @click="addTask"><i class="fa fa-plus" aria-hidden="true"></i></button>
            </div>
            <div class="task-list">
                <SingleTask 
                    v-for="(task, key) in taskArr"
                    :key="key+task"
                    :id="key"
                    :value="task"
                    @removeTask="removeTask"
                    @updateTask="updateTask"
                />
            </div>
      </div>
  </div>
</template>

<script>

import SingleTask from "./SingleTask.vue";
export default {
  name: "Home",
  components: {
    SingleTask
  },
  data() {
    return {
      newTask: "",
      taskArr: []
    };
  },
  created(){
      
      if(  localStorage.getItem("taskArrLocalStorage") != null ){
          this.taskArr = JSON.parse(localStorage.getItem("taskArrLocalStorage"))
      }
  },
  methods: {
    addTask() {
        if(this.newTask != ''){
            this.taskArr.push(this.newTask);
            localStorage.setItem("taskArrLocalStorage", JSON.stringify(this.taskArr));
            this.newTask = '';
        }else{
            alert('pusty task!')
        }
    },
    removeTask(id) {
      this.taskArr.splice(id, 1);
      localStorage.setItem("taskArrLocalStorage", JSON.stringify(this.taskArr));
    },
    updateTask(id,newValue){
        this.$set(this.taskArr,id, newValue)
        localStorage.setItem("taskArrLocalStorage", JSON.stringify(this.taskArr));
    }
  }
};
</script>

