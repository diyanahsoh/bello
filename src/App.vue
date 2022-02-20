<template>
  <div id="app" class="container mt-3">
    <div class="row">
      <h1>Bello - Kanban Board</h1>
      <div class="col">
        <b-form-input id="inline-form-input-name" class="mb-2 mr-sm-2 mb-sm-0" v-model="name" placeholder="Board Name"
          style="font-size: 30px"></b-form-input>
      </div>
      <div class="col">
        <b-form-textarea id="textarea" v-model="description" placeholder="Board Description" rows="1" max-rows="4">
        </b-form-textarea>
      </div>
      <div class="col-3">
        <b-form inline>
        </b-form>
      </div>
    </div>
    <div class="row mt-5">
      <div class="col">
        <div class="p-3 alert alert-primary">
          <h3>To-Do</h3>
          <draggable class="list-group kanban-column" :list="arrTodo" group="tasks">
            <Card v-for="cards in arrTodo" v-bind:key="cards.name" v-bind:name="cards.name" @on-delete="onDelete" />
          </draggable>
          <b-form inline v-if="addNew">
            <b-form-input id="inline-form-input-name" class="mb-2 mr-sm-2 mb-sm-0" v-model="newCard"
              placeholder="Enter Task" @keyup.enter="addCard" style="display: inline; width: inherit; margin-right: 20px;">
            </b-form-input>
            <b-button variant="success" class="ml-3" @click="addCard()">
              Add
            </b-button>
          </b-form>
          <b-button v-else variant="primary" class="ml-3" @click="addNew=true">
            Add new card
          </b-button>
        </div>
      </div>

      <div class="col">
        <div class="p-3 alert alert-warning">
          <h3>In Progress</h3>
          <draggable class="list-group kanban-column" :list="arrInProgress" group="tasks">
            <Card v-for="cards in arrInProgress" v-bind:key="cards.name" v-bind:name="cards.name" @on-delete="onDelete" />
          </draggable>
          <b-form inline v-if="addProg">
            <b-form-input id="inline-form-input-name" class="mb-2 mr-sm-2 mb-sm-0" v-model="progCard"
              placeholder="Enter Task" style="display: inline; width: inherit; margin-right: 20px;">
            </b-form-input>
            <b-button variant="success" class="ml-3" @click="addCard()">
              Add
            </b-button>
          </b-form>
          <b-button v-else variant="primary" class="ml-3" @click="addProg=true">
            Add new card
          </b-button>
        </div>
      </div>

      <div class="col">
        <div class="p-3 alert alert-success">
          <h3>Done</h3>
          <draggable class="list-group kanban-column" :list="arrDone" group="tasks">
            <Card v-for="cards in arrDone" :key="cards.name" :name="cards.name" :board="arrDone" @on-delete="onDelete" />
          </draggable>
          
          <b-form inline v-if="addDone">
            <b-form-input id="inline-form-input-name" class="mb-2 mr-sm-2 mb-sm-0" v-model="doneCard"
              placeholder="Enter Task" style="display: inline; width: inherit; margin-right: 20px;">
            </b-form-input>
            <b-button variant="success" class="ml-3" @click="addCard()">
              Add
            </b-button>
          </b-form>
          <b-button v-else variant="primary" class="ml-3" @click="addDone=true">
            Add new card
          </b-button>
        </div>
      </div>
    </div>
    <KanbanColumn />
  </div>
</template>

<script>
import draggable from "vuedraggable";
import KanbanColumn from "./components/KanbanColumn.vue";
import Card from "./components/Card.vue";

export default {
  name: 'App',
  components: {
    draggable,
    KanbanColumn,
    Card
  },
  data() {
    return {
      name: "",
      description: "",
      newCard: "",
      progCard: "",
      doneCard: "",
      addNew: false,
      addProg: false,
      addDone: false,
      arrTodo: [
        { name: "Code Sign Up Page" },
        { name: "Help with Designs" }
      ],
      arrInProgress: [],
      arrDone: []
    };
  },
  methods: {
    addCard() {
      if (this.newCard) {
        this.arrTodo.push({
          name: this.newCard
        });
        this.newCard = "";
        this.addNew = false;
      }
      if (this.progCard) {
        this.arrInProgress.push({
          name: this.progCard
        });
        this.progCard = "";
        this.addProg = false;
      }
      if (this.doneCard) {
        this.arrDone.push({
          name: this.doneCard
        });
        this.doneCard = "";
        this.addDone = false;
      }
    },
    onDelete(cardText, board) {
      console.log(board);
      var index = board.indexOf(cardText);
      if (index > -1) {
        board.splice(index, 1);
      }
      return board;
      // alert(`Deleting ${cardText}`);
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
}
.kanban-column {
  min-height: 300px;
}
</style>
