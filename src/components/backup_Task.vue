<template>
  <div>
    <v-flex>
      <v-card width="300px" height="200px" class="ml-5 my-5">
        <v-form class="ml-4 white">
          <v-text-field label="タイトル" v-model="newTask.title" />
          <v-text-field type="date" label="期限" v-model="newTask.due" />
          <v-card-actions @click="addTask">
            <v-btn style="text-transform: none">Add</v-btn>
          </v-card-actions>
        </v-form>
      </v-card>

      <v-list-item v-for="(task, index) in tasks" :key="index">
        <v-card width="300px" height="150px" class="mx-1 my-1">
          <v-card-title>{{ task.title }}</v-card-title>
          <v-card-text>{{ task.due }} {{ task.status }}</v-card-text>
          <v-btn class="mx-4" x-small @click="editTask(index)">edit</v-btn>
          <v-btn x-small @click="deleteTask(index)">×</v-btn>
        </v-card>
      </v-list-item>
    </v-flex>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      newTask: {
        title: "",
        due: "",
        status: ""
      },
      tasks: [
        {
          title: "aaa",
          due: "dd",
          status: "未了"
        }
      ]
    };
  },
  watch: {
    tasks: {
      handler: function () {
        localStorage.setItem("tasks", JSON.stringify(this.tasks));
      },
      deep: true
    }
  },
  mounted: function () {
    this.tasks = JSON.parse(localStorage.getItem("tasks")) || [];
  },
  methods: {
    addTask () {
      this.newTask.status = "未了";
      this.tasks.push(this.newTask);
      this.newTask = {};
    },
    editTask (index) {
      index;
    },
    deleteTask (index) {
      if (confirm("are you sure?")) {
        this.tasks.splice(index, 1);
      }
    }
  }
};
</script>
