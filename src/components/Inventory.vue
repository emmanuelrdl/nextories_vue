<template>
  <div>
    <b-card>
      <div v-for="fourniture in fournitures">
        <div style="display: flex;justify-content: space-between;">
          <input
            type="checkbox"
            :id="fourniture.id"
            :checked="false"
            @change="changeRemovalState(fourniture, $event)">
          <div >{{fourniture.id}}</div>
          <div >{{fourniture.name}}</div>
          <div @click="removeFourniture(fourniture)">x</div>
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
      if (event.target.checked) {
        this.fournitureIdsForRemoval.push(fourniture.id);
      } else {
        var index = this.fournitureIdsForRemoval.indexOf(fourniture.id);
        this.fournitureIdsForRemoval.splice(index, 1);
      }
      this.$emit("updateFournitureIdsForRemoval", this.fournitureIdsForRemoval)
    }
  }
}
</script>
