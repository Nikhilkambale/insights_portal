<template>
<div class="dropdown">
  <button class="btn btn-secondary dropdown-toggle" type="button" id="dropdownMenuButton1" data-bs-toggle="dropdown" aria-expanded="false">
    Dropdown button
  </button>
  <ul class="dropdown-menu" aria-labelledby="dropdownMenuButton1">
    <li><a class="dropdown-item" href="#" @click="selectOption('image')">Image</a></li>
    <li><a class="dropdown-item" href="#" @click="selectOption('image')">Chart</a></li>
    <li><a class="dropdown-item" href="#" @click="selectOption('image')">Textbox</a></li>
    <li><a class="dropdown-item" href="#" @click="selectOption('image')">File</a></li>
  </ul>
</div>

<div v-if="selectedOption === 'image'">
  <ImageComponent />
</div>
<div v-if="selectedOption === 'chart'">
  <ChartComponent />
</div>
<div v-if="selectedOption === 'textbox'">
  <TextboxComponent />
</div>
<div v-if="selectedOption === 'file'">
  <FileComponent />
</div>


  <div class="test">
  <div>
    <input type="text" v-model="selectedCard.heading" />
  </div>
  <div>
    <input type="text" v-model="selectedCard.description" />
  </div>
</div>
  <button type="button" class="btn btn-primary" style="margin: 2em;" @click="submitEditForm">Submit</button>

</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      cardId: this.$route.params.id
    };
  },
  methods: {
    submitEditForm() {
      const response = axios.put(`http://localhost:3000/cards/${this.cardId}`, this.selectedCard);
      console.log(response)
      this.$router.push({
        name: "about"
      });
    },
  },
  computed: {
    cards() {
      return this.$store.state.cards;
    },
    selectedCard() {
      const card = this.cards.find((card) => String(card.id) === this.cardId);
      console.log(card);
      return card;
    },
  },
  
 
  
};
</script>

<style>
.dropdown{
  display: flex;
}
.test{
  display: grid;
    justify-content: center;
    gap: 1em;
}
</style>