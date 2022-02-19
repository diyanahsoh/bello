<template>
  <div id="app" class="container mt-5">
    <div class="row">
      <h1>Bello - Kanban Board</h1>
      <div class="col">Board Name</div>
      <div class="col">Board Description</div>
      <div class="col-3 form-inline">
        <b-form-input v-model="newTask" placeholder="Enter Task" @keyup.enter="add">
        </b-form-input>
        <b-button @click="add" variant="primary" class="ml-3">
          Add
        </b-button>
      </div>
    </div>
  <div class="row mt-5">
    <div class="col-3">
      <div class="p-2 alert alert-secondary">
        <h3>To-Do</h3>
        <draggable class="list-group kanban-column" :list="arrTodo" group="tasks">
          <div class="list-group-item" v-for="element in arrTodo" :key="element.name">
            {{ element.name }}
          </div>
        </draggable>
      </div>
    </div>
    <div class="col-3">
      <div class="p-2 alert alert-primary">
        <h3>In Progress</h3>
        <draggable class="list-group kanban-column" :list="arrInProgress" group="tasks">
          <div class="list-group-item" v-for="element in arrInProgress" :key="element.name">
            {{ element.name }}
          </div>
        </draggable>
      </div>
    </div>
    <div class="col-3">
      <div class="p-2 alert alert-success">
        <h3>Done</h3>
        <draggable class="list-group kanban-column" :list="arrDone" group="tasks">
          <div class="list-group-item" v-for="element in arrDone" :key="element.name">
            {{ element.name }}
          </div>
        </draggable>
      </div>
    </div>
  </div>
    <KanbanColumn />
  </div>
</template>

<script>
import KanbanColumn from "./components/KanbanColumn.vue";
import draggable from "vuedraggable";

export default {
  name: 'App',
  components: {
    KanbanColumn,
    draggable
  },
  data() {
    return {
      newCard: "",
      arrTodo: [
        { name: "Code Sign Up Page" },
        { name: "Test Dashboard" },
        { name: "Style Registration" },
        { name: "Help with Designs" }
      ],
      arrInProgress: [],
      arrDone: []
    };
  },
  methods: {
    addCard() {
      if (this.newCard) {
        this.arrTodo.push({ name: this.newCard });
        this.newCard = "";
      }
    }
}
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Comfortaa&display=swap');
#app {
  font-family: 'Comfortaa', cursive;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /* padding: 50px; */
}
.kanban-column {
  min-height: 300px;
}
</style>
