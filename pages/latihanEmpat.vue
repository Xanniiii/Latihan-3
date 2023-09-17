<template>
  <div class="py-4">
    <div class="container">
      <div class="title border-bottom d-flex align-items-center justify-content-between py-2">
        <h5>Task</h5>
        <div class="d-flex align-items-center">
          <input
            type="text"
            class="form-control"
            placeholder="Search"
            v-model="searchQuery"
          />
          <div class="d-flex align-items-center justify-content-end w-100">
            <span class="me-2">View As</span>
            <button
              class="btn btn-outline-secondary py-1 px-3"
              @click="isGrid=!isGrid"
            >
              {{ isGrid ? 'Grid' : 'List' }}
            </button>
          </div>
        </div>
      </div>
      <div class="list-task row">
        <CardItem
          v-for="(task, i) in resultQuery"
          :key="i"
          :task="task"
          :isGrid="isGrid"
        />
      </div>
      <div class="action py-2">
        <a
          v-if="!isCreating"
          href="#"
          class="add-button"
          @click="isCreating=!isCreating"
        >
          Add Task
        </a>
        <form v-else class="add-card" @submit.prevent="addTask">
          <div class="card mb-2">
            <div class="card-body d-flex flex-column p-0">
              <input
                v-model="newTask.title"
                class="form-control border-0 mb-2"
                placeholder="Title"
                type="text"
              />
              <textarea
                v-model="newTask.description"
                class="form-control border-0 small"
                placeholder="Description"
                rows="3"
              ></textarea>
            </div>
          </div>
          <div class="button-wrapper d-flex">
            <button class="btn btn-primary me-2" type="submit">Save</button>
            <button
              class="btn btn-outline-secondary"
              @click="cancelAddTask"
            >
              Cancel
            </button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import CardItem from "@/components/Card/CardItem.vue";
export default {
  layout(context) {
    return "custom";
  },
  components: {
    CardItem,
  },
  data() {
    return {
      searchQuery: "",
      isGrid: true,
      isCreating: false,
      newTask: {
        title: "",
        description: "",
        isDone: false,
      },
      tasks: [],
    };
  },
  computed: {
    resultQuery() {
      if (this.searchQuery) {
        return this.tasks.filter((item) => {
          return this.searchQuery
            .toLowerCase()
            .split(" ")
            .every((v) => item.title.toLowerCase().includes(v));
        });
      } else {
        return this.tasks;
      }
    },
  },
  methods: {
    addTask() {
      if (this.newTask.title.trim() === "") return;

      this.tasks.push({ ...this.newTask });
      this.newTask.title = "";
      this.newTask.description = "";
      this.isCreating = false;
    },
    cancelAddTask() {
      this.newTask.title = "";
      this.newTask.description = "";
      this.isCreating = false;
    },
  },
};
</script>
