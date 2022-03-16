<template>
  <b-container id="app" class="background" fluid>
    <div class="cube"></div>
    <div class="cube"></div>
    <div class="cube"></div>
    <div class="cube"></div>
    <div class="cube"></div>
    <b-row>
      <b-col cols="12"><h1 class="mt-3" style="color: white">Bello - Kanban Board</h1></b-col>
      <b-col>
        <b-form-input id="inline-form-input-name" class="mb-2 mr-sm-2 mb-sm-0" v-model="name" placeholder="Board Name"
          style="font-size: 30px"></b-form-input>
      </b-col>
      <b-col>
        <b-form-textarea id="textarea" v-model="description" placeholder="Board Description" rows="1" max-rows="4">
        </b-form-textarea>
      </b-col>
    </b-row>
    <b-row class="mt-4">
      <b-col>
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
      </b-col>

      <b-col>
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
      </b-col>

      <b-col>
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
      </b-col>
    </b-row>
  </b-container>
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
  width: inherit;
  /* border: 2px solid red; */
}
.container {
  border: 2px solid blue;
}
.kanban-column {
  min-height: 300px;
  min-width: 250px;
}
/* ============= Animation background ========= */
.background {
  background: linear-gradient(132deg, #3b3d54, #591BC5, #212335);
  background-size: 400% 400%;
  animation: Gradient 15s ease infinite;
  position: relative;
  height: 100vh;
  width: 100%;
  overflow: hidden;
  padding:0;
  margin:0px;
}
.cube {
  position: absolute;
  top: 80vh;
  left: 45vw;
  width: 10px;
  height: 10px;
  border: solid 1px #D7D4E4;
  transform-origin: top left;
  transform: scale(0) rotate(0deg) translate(-50%, -50%);
  animation: cube 12s ease-in forwards infinite;
}
.cube:nth-child(2n) {
  border-color: #FFF ;
}
.cube:nth-child(2) {
  animation-delay: 2s;
  left: 25vw;
  top: 40vh;
}
.cube:nth-child(3) {
  animation-delay: 4s;
  left: 75vw;
  top: 50vh;
}
.cube:nth-child(4) {
  animation-delay: 6s;
  left: 90vw;
  top: 10vh;
}
.cube:nth-child(5) {
  animation-delay: 8s;
  left: 10vw;
  top: 85vh;
}
.cube:nth-child(6) {
  animation-delay: 10s;
  left: 50vw;
  top: 10vh;
}
/* Animate Background*/
@keyframes Gradient {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}
@keyframes cube {
  from {
    transform: scale(0) rotate(0deg) translate(-50%, -50%);
    opacity: 1;
  }
  to {
    transform: scale(20) rotate(960deg) translate(-50%, -50%);
    opacity: 0;
  }
}
</style>
