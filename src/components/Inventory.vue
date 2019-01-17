<template>
  <div>
    <b-card>
      <div v-for="fourniture in fournitures">
        <div class="flex-card-header">
          <div class="checkbox" @click="changeRemovalState(fourniture, $event)">
            <span v-if="fourniture.selectedForDeletion">v</span>
          </div>
          <div >{{fourniture.name}}</div>
          <div class="btn-delete" @click="removeFourniture(fourniture)">x</div>
        </div>
      </div>
    </b-card>
  </div>
</template>

<script>
export default {
  props: ["fournitures"],
  data () {
    return {
      fournitureIdsForRemoval: [],
    }
  },
  methods: {
    removeFourniture(fourniture){
      this.$emit("removeFourniture", fourniture.id);
    },
    changeRemovalState(fourniture, event){
      fourniture.selectedForDeletion = !fourniture.selectedForDeletion;
      if (fourniture.selectedForDeletion) {
        this.fournitureIdsForRemoval.push(fourniture.id);
      } else {
        var index = this.fournitureIdsForRemoval.indexOf(fourniture.id);
        this.fournitureIdsForRemoval.splice(index, 1);
      }
      this.$emit("updateFournitureIdsForRemoval", this.fournitureIdsForRemoval);
    }
  }
}
</script>
