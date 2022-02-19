<template>
  <div class="row mt-5">
    <!-- <div class="col-3">
      <div class="p-2 alert alert-secondary">
        <h3>Back Log</h3>
        <draggable class="list-group kanban-column" :list="arrBackLog" group="tasks">
          <div class="list-group-item" v-for="element in arrBackLog" :key="element.name">
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
      <div class="p-2 alert alert-warning">
        <h3>Testing</h3>
        <draggable class="list-group kanban-column" :list="arrTested" group="tasks">
          <div class="list-group-item" v-for="element in arrTested" :key="element.name">
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
    </div> -->
  </div>
</template>

<script>
// import draggable from "vuedraggable";

export default {
  name: 'KanbanColumn',
  components: {
    // draggable
  },
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
