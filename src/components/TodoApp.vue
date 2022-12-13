<template>
  <div class="container">
    <h2 class="text-center mt-5">A Simple Vue Todo App</h2>

    <!--    input  -->
    <div class="d-flex">
      <input
        v-model="task"
        type="text"
        class="form-control"
        placeholder="Enter text"
      />

      <button class="btn btn-warning rounded-0" @click="submitTask()">
        Submit
      </button>
    </div>
    <p class="text-danger" v-if="show">Please enter text</p>

    <!--- Task Table -->
    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col" class="text-primary">Task</th>
          <th scope="col" class="text-primary">Status</th>
          <th scope="col" class="text-center text-primary">Edit</th>
          <th scope="col" class="text-center text-primary">Delete</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <th scope="row">
            <span :class="{'finished': task.status === 'finished'}">{{ task.name }}</span></th>
          <td class="size"><span class="pointer" @click="setStatus(index)"><a class="text-primary" href="#">{{ task.status }}</a></span></td>
          <td>
            <div class="text-center text-success" @click="editTask(index)">
              <span class="fa fa-pen"></span>
            </div>
          </td>
          <td>
            <div class="text-center text-danger" @click="deleteTask(index)">
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
  data() {
    return {
      show: false,
      task: "",
      editTasks: null,
      availableStatus:["to-do","pending","finished"],
      tasks: [
        {
          name: "Buy Banana from the store",
          status: "to-do",
        },
        {
          name: "Buy chocolate ",
          status: "in-progress",
        },
      ],
    };
  },
  methods: {
    submitTask() {
      if (this.task.length === 0) {
        this.show = true;
      }
      if (this.editTasks === null) {
        this.tasks.push({
          name: this.task,
          status: "to-do",
        });
      } else {
        this.tasks[this.editTasks].name = this.task;
        this.editTasks = null;
      }
      this.show = false;
      this.task = "";
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    editTask(index) {
      this.task = this.tasks[index].name;
      this.editTasks = index;
    },
    setStatus(index){
        let newIndex = this.availableStatus.indexOf(this.tasks[index].status)
        if(++newIndex > 2) newIndex = 0
        this.tasks[index].status = this.availableStatus[newIndex]
    }
  },
};
</script>

<style scoped>
.pointer{
    cursor: pointer;
}
.size{
    width: 120px;
}
.finished{
    text-decoration: line-through;
}
</style>
