<template>
  <div id="app" class="container vh-100">
    <div class="row">
      <div class="col-12"><h1 class="mt-3">Bello - Kanban Board</h1></div>
      <div class="col">
        <b-form-input id="inline-form-input-name" class="mb-2 mr-sm-2 mb-sm-0" v-model="name" placeholder="Board Name"
          style="font-size: 30px"></b-form-input>
      </div>
      <div class="col">
        <b-form-textarea id="textarea" v-model="description" placeholder="Board Description" rows="1" max-rows="4">
        </b-form-textarea>
      </div>
    </div>
    <div class="row mt-4">
      <div class="col">
        <div class="p-3 alert-primary">
          <h3>To-Do</h3>
          <draggable class="list-group kanban-column" :list="arrTodo" group="tasks">
            <Card v-for="cards in arrTodo" :key="cards.name" :name="cards.name" :board="arrTodo" @on-edit="onEdit" @on-delete="onDelete" />
          </draggable>
          <b-form inline v-if="addTodo" class="mt-3">
            <b-form-input id="inline-form-input-name" class="mb-2 mr-sm-2 mb-sm-0" v-model="todoCard"
              placeholder="Enter Task" style="display: inline; width: inherit; margin-right: 20px;">
            </b-form-input>
            <b-button variant="success" class="ml-3" @click="addCard()">
              Add
            </b-button>
          </b-form>
          <b-button v-else variant="primary" class="mt-3" @click="addTodo=true">
            Add new card
          </b-button>
        </div>
        <b-alert show variant="primary">Max No. Cards: {{ maxTodo }}
          <b-form inline v-if="editTodo">
            <b-form-input class="mb-2 mr-sm-2 mb-sm-0" v-model="todoNum"
              placeholder="Num" style="max-width: 100px;" type="number">
            </b-form-input>
            <b-button variant="success" @click="maxTodo=todoNum, todoNum='', editTodo=false">
              Confirm
            </b-button>
          </b-form>
          <b-button v-else variant="info" class="ml-3" @click="editTodo=true">
            Edit Max No.
          </b-button>
        </b-alert>
      </div>

      <div class="col">
        <div class="p-3 alert-warning">
          <h3>In Progress</h3>
          <draggable class="list-group kanban-column" :list="arrInProgress" group="tasks"><!--  :move="checkMove" -->
            <Card v-for="cards in arrInProgress" :key="cards.name" :name="cards.name" :board="arrInProgress" @on-edit="onEdit" @on-delete="onDelete" />
          </draggable>
          <b-form inline v-if="addProg" class="mt-3">
            <b-form-input id="inline-form-input-name" class="mb-2 mr-sm-2 mb-sm-0" v-model="progCard"
              placeholder="Enter Task" style="display: inline; width: inherit; margin-right: 20px;">
            </b-form-input>
            <b-button variant="success" class="ml-3" @click="addCard()">
              Add
            </b-button>
          </b-form>
          <b-button v-else variant="primary" class="mt-3" @click="addProg=true">
            Add new card
          </b-button>
        </div>
        <b-alert show variant="warning">Max No. Cards: {{ maxProg }}
          <b-form inline v-if="editProg">
            <b-form-input class="mb-2 mr-sm-2 mb-sm-0" v-model="progNum"
              placeholder="Num" style="max-width: 100px;" type="number">
            </b-form-input>
            <b-button variant="success" @click="maxProg=progNum, progNum='', editProg=false">
              Confirm
            </b-button>
          </b-form>
          <b-button v-else variant="info" class="ml-3" @click="editProg=true">
            Edit Max No.
          </b-button>
        </b-alert>
      </div>

      <div class="col">
        <div class="p-3 alert-success">
          <h3>Done</h3>
          <draggable class="list-group kanban-column" :list="arrDone" group="tasks">
            <Card v-for="cards in arrDone" :key="cards.name" :name="cards.name" :board="arrDone" @on-edit="onEdit" @on-delete="onDelete" />
          </draggable>
          <b-form inline v-if="addDone" class="mt-3">
            <b-form-input class="mb-2 mr-sm-2 mb-sm-0" v-model="doneCard"
              placeholder="Enter Task" style="display: inline; width: inherit; margin-right: 20px;">
            </b-form-input>
            <b-button variant="success" class="ml-3" @click="addCard()">
              Add
            </b-button>
          </b-form>
          <b-button v-else variant="primary" class="mt-3" @click="addDone=true">
            Add new card
          </b-button>
        </div>
        <b-alert show variant="success">Max No. Cards: {{ maxDone }}
          <b-form inline v-if="editDone">
            <b-form-input class="mb-2 mr-sm-2 mb-sm-0" v-model="doneNum"
              placeholder="Num" style="max-width: 100px;" type="number">
            </b-form-input>
            <b-button variant="success" @click="maxDone=doneNum, doneNum='', editDone=false">
              Confirm
            </b-button>
          </b-form>
          <b-button v-else variant="info" class="ml-3" @click="editDone=true">
            Edit Max No.
          </b-button>
        </b-alert>
      </div>
    </div>
  </div>
</template>

<script>
import draggable from "vuedraggable";
import Card from "./components/Card.vue";

export default {
  name: 'App',
  components: {
    draggable,
    Card
  },
  data() {
    return {
      name: "",
      description: "",
      todoCard: "",
      progCard: "",
      doneCard: "",
      addTodo: false,
      addProg: false,
      addDone: false,
      maxTodo: 5,
      maxProg: 5,
      maxDone: 5,
      editTodo: false,
      editProg: false,
      editDone: false,
      arrTodo: [
        { name: "Code Sign Up Page" },
        { name: "Help with Designs" }
      ],
      arrInProgress: [],
      arrDone: []
    };
  },
  mounted() {
    if (localStorage.name) {
      this.name = localStorage.name;
    } else {
      localStorage.name = this.name;
    }
    if (localStorage.description) {
      this.description = localStorage.description;
    } else {
      localStorage.description = this.description;
    }
  },
  methods: {
    addCard() {
      if (this.todoCard && this.arrTodo.length < this.maxTodo) {
        this.arrTodo.push({
          name: this.todoCard
        });
        this.todoCard = "";
        this.addTodo = false;
      }
      if (this.progCard && this.arrInProgress.length < this.maxProg) {
        this.arrInProgress.push({
          name: this.progCard
        });
        this.progCard = "";
        this.addProg = false;
      }
      if (this.doneCard && this.arrDone.length < this.maxDone) {
        this.arrDone.push({
          name: this.doneCard
        });
        this.doneCard = "";
        this.addDone = false;
      }
    },
    onEdit(user) {
      alert(`Editing ${user.name}`);
    },
    onDelete(cardText, board) {
      var index = this.getIndex(board, cardText);
      console.log(index);
      if (index > -1) {
        board.splice(index, 1);
      }
      return board;
    },
    getIndex(array, text) {
      for (let i = 0; i < array.length; i++) {
        if (text == array[i].name) {
          return i
        }
      }
    },
		checkMove: function(evt) { //https://github.com/SortableJS/Vue.Draggable/issues/45
			// if (evt.draggedContext.element.name=='test'){
			// 	return false
			// }
      console.log(evt.relatedContext);
			if (evt.relatedContext.list.length==this.maxProg){
				return false
			}
			return true;
		},
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
  /* background-image: linear-gradient(to bottom right, white, blue); */
}
.kanban-column {
  min-height: 300px;
  min-width: 250px;
}
</style>
