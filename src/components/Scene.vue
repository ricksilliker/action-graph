<template>
<div class="scene" id="scene-graph">
  <div id="tool-bar">
    <div id="add-card-btn" v-on:click="addNewCard">Add Card</div>
  </div>
  <div id="card-list" v-on:click="deselectCards">
    <Card v-for="card in cards"
          :key="card.cardId"
          v-bind:selected="card.selected"
          v-bind:title="card.title"/>
  </div>
</div>
</template>

<script>
const uuid = require('uuid');
import Card from "@/components/Card";

export default {
  name: "Scene",
  components: {Card},
  data: function() {
    return {
      currentCard: null,
      cards: [],
      ctrlModifierPressed: false
    }
  },
  methods: {
    deselectCards: function(e) {
      if (e.ctrlKey) {
        return;
      }
      if (e.target.id === "card-list") {
        this.cards.forEach(c => {
          c.selected = false;
        });
      }
      this.currentCard = null;
    },
    addNewCard: function() {
      this.cards.push({
        title: "New Card",
        cardId: uuid.v4(),
        selected: false,
        xPos: 0,
        yPos: 0,
      })
    },
    handleCardSelection: function(card) {
      this.cards.forEach(c => {
        c.selected = false;
      });
      card.selected = true;
      this.currentCard = card;
    },
  }
}
</script>

<style scoped>
.scene {
  background: #454545;
  width: 1280px;
  height: 760px;
}

#card-list {
  width: 100%;
  height: 100%;
  overflow: hidden;
}

#add-card-btn {
  background: white;
  border: 1px solid black;
  color: black;
  cursor: pointer;
}
</style>