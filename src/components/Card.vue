<template>
<div v-bind:class="cardStyleClass">
  {{ title }}
</div>
</template>

<script>
export default {
  name: "Card",
  props: ["title", "cardId", "selected", "xPos", "yPos"],
  data: function() {
    return {
      // isSelected: this.selected,
    }
  },
  computed: {
    cardStyleClass: function() {
      return {
        deselectedCard: !this.isSelected,
        selectedCard: this.isSelected
      }
    },
    isSelected: function() {
      return this.selected;
    }
  },
  methods: {
    selectCard: function() {
      this.isSelected = true;
    },
    deselectCard: function() {
      this.isSelected = false;
    }
  }
}
</script>

<style scoped>

.selectedCard {
  position: absolute;
  background: mediumseagreen;
  border: 5px solid goldenrod;
  color: whitesmoke;
  border-radius: 5px;
  width: 200px;
  height: 150px;
}

.deselectedCard {
  position: absolute;
  background: mediumseagreen;
  color: whitesmoke;
  border-radius: 5px;
  width: 200px;
  height: 150px;
}
</style>