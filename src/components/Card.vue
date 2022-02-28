<template>
    <b-list-group-item class="d-flex justify-content-between align-items-center cursor-move">
        <p class="ml-3 card-text">{{ cardText }}</p>
        <!-- <b-icon icon="pencil-square" scale="2" variant="success" @click="$emit('on-edit', cardText, board)"></b-icon> -->
        <b-icon icon="trash" scale="2" variant="danger" @click="$emit('on-delete', cardText, board)"></b-icon>
    </b-list-group-item> 
</template>

<script>
  export default {
    name: 'Card',
    props: {
      name: String,
      board: Array
    },
    data () {
      return {
        cardText: this.name
      }
    },
  }
</script>

<style scoped>
.card-text{
  min-width: 250px;
  text-align: left;
}
.b-icon {
  cursor: pointer;
}
</style>