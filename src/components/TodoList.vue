<template>
  <div class="container">
   <h1 class="text-center mt-5">ĐẶNG MINH TÍNH</h1>
   <div class="d-flex">
    <input v-model=task type="text" placeholder="Nhập vào đây" class="form-control">
    <button class="btn btn-success rounded mx-3" @click="submitTask()">Submit</button>
   </div>
   <table class="table">
  <thead>
    <tr>
      <th scope="col">Task</th>
      <th scope="col">Status</th>
      <th scope="col" class="text-center">Action</th>
      <th scope="col" class="text-center">#</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(task, index) in tasks" :key="index">
      <td>{{ task.name }}</td>
      <td>
        <div @click="changeStatus(index)" class="cursor-pointer">
          {{ task.status }}
        </div>
      </td>
      <td>
        <div class="text-center cursor-pointer" @click="editTask(index)">
          <span class="fa fa-pen"></span>
        </div>
      </td>
      <td>
        <div class="text-center cursor-pointer" @click="deleteTask(index)">
          <span class="fa fa-trash"></span>
        </div>
      </td>
    </tr>
    
  </tbody>
</table>
  </div>
</template>

<script>
export default {
  name: 'TodoList',
  data() {
    return {
      task: '',
      editedTask: null,
      avalableStatus: ['Cần làm', 'Đang làm', 'hoàn thành'],
      tasks: [
        {
          name: 'Task 1',
          status: 'Cần làm',
        },
        {
          name: 'Task 2',
          status: 'Đang làm',
        }
      ]
    }
  },
  methods: {
    submitTask() {
      if (this.task.length === 0) return;

      if (this.editedTask === null) {
        this.tasks.push({
          name: this.task,
          status: 'Cần làm'
        });
      } else {
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = null;
      }

      this.task = '';
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    editTask(index) {
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },
    changeStatus(index) {
      let newIndex = this.avalableStatus.indexOf(this.tasks[index].status);

      if (++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.avalableStatus[newIndex];
    }
  } 
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.cursor-pointer {
  cursor: pointer;
}
</style>
