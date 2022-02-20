<template>
    <b-list-group-item class="d-flex justify-content-between align-items-center">
        <!-- <b-form-textarea id="textarea" :value="cardDescription" placeholder="Add Card" rows="1" max-rows="4">
        </b-form-textarea> 
        <b-form-textarea id="textarea-plaintext" class="card-text" plaintext :value="cardText"></b-form-textarea>-->
        <p class="ml-2">{{ cardText }}</p>
        <b-icon icon="pencil-square" scale="2" variant="success"></b-icon>
        <b-icon icon="trash" scale="2" variant="danger"></b-icon>
    </b-list-group-item> 
    <!-- <div class="list-group-item">
        <h5>{{ this.name }}</h5>
        <p class="ml-2">{{ cardText }}</p>
    </div>-->
</template>

<script>
  export default {
    name: 'Card',
    props: {
      name: String,
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
    margin-right: 20px;
    max-width: 250px;
}
</style>