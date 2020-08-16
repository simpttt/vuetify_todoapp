<template>
  <div>
    <v-container>
      <v-row>
        <v-col cols="12" sm="6" md="6" lg="6">
          <v-card>
            <v-form class="mx-4">
              <v-text-field label="タイトル" v-model="newTask.title" />
              <v-text-field type="date" label="期限" v-model="newTask.due" />
              <v-card-actions @click="addTask">
                <v-btn style="text-transform: none">Add</v-btn>
              </v-card-actions>
            </v-form>
          </v-card>
        </v-col>

        <v-col cols="12" sm="6" md="6" lg="6">
          <v-list-item v-for="(task, index) in tasks" :key="index">
            <v-card class="mb-4">
              <v-card-title>{{ task.title }}</v-card-title>
              <v-card-text>{{ task.due }} {{ task.status }}</v-card-text>
              <v-btn class="mx-4" x-small @click="editTask(index)">edit</v-btn>
              <v-btn x-small @click="deleteTask(index)">×</v-btn>
            </v-card>
          </v-list-item>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
export default {
  data: function() {
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
      handler: function() {
        localStorage.setItem("tasks", JSON.stringify(this.tasks));
      },
      deep: true
    }
  },
  mounted: function() {
    this.tasks = JSON.parse(localStorage.getItem("tasks")) || [];
  },
  methods: {
    addTask() {
      this.newTask.status = "未了";
      this.tasks.push(this.newTask);
      this.newTask = {};
    },
    editTask(index) {
      index;
    },
    deleteTask(index) {
      if (confirm("are you sure?")) {
        this.tasks.splice(index, 1);
      }
    }
  }
};
</script>
