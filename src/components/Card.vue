<template>
    <b-list-group-item class="d-flex justify-content-between align-items-center cursor-move">
        <!-- <b-form-textarea id="textarea" :value="cardDescription" placeholder="Add Card" rows="1" max-rows="4">
        </b-form-textarea> 
        <b-form-textarea id="textarea-plaintext" class="card-text" plaintext :value="cardText"></b-form-textarea>-->
        <p class="ml-3 card-text">{{ cardText }}</p>
        <b-icon icon="pencil-square" scale="2" variant="success"></b-icon>
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
    methods: {
      onEdit(user) {
        alert(`Editing ${user.name}`);
      }
    }
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