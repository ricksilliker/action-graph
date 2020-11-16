<template>
<div v-bind:class="cardStyleClass" v-bind:style="{ top: yPos + 'px', left: xPos + 'px'}" @mousedown="enableDragCard" @mousemove="dragCard" @mouseup="disableDragCard">
  {{ title }}
</div>
</template>

<script>
export default {
  name: "Card",
  props: ["title", "cardId", "selected"],
  data: function() {
    return {
      dragEnabled: false,
      xPos: 0,
      yPos: 0,
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
    },
    enableDragCard: function() {
      console.log('enable drag');
      this.dragEnabled = true;
    },
    disableDragCard: function() {
      console.log('disable drag');
      this.dragEnabled = false;
      console.log(this.xPos, this.yPos);
    },
    dragCard: function(e) {
      if (!this.dragEnabled) { return; }
      console.log('is dragging');
      this.xPos = e.x - 50;
      this.yPos = e.y - 50;
    }
  }
}
</script>

<style scoped>

.selectedCard {
  cursor: move;
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