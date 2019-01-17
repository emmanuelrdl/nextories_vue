<template>
  <div id="app">
    <b-container class="bv-example-row">
      <b-row>
          <b-col cols="7">
            <Form
              v-on:newFourniture="addNewFourniture"
              v-bind:fournitures="fournitures"
            />
          </b-col>
          <b-col cols="5"></b-col>
      </b-row>
      <b-row>
          <b-col cols="12">
            <div class="flex-card-header">
              <h2 class="pull-left">
                Inventaire
                <span class="btn-global-delete" @click="removeFournitures">x</span>
              </h2>
              <h2 class="pull-right">
                Volume Total:
                <span class="total-volume-card">{{totalVolume.toFixed(2)}} m3</span>
              </h2>
            </div>
            <Inventory
              v-bind:fournitures="fournitures"
              v-on:removeFourniture="removeFourniture"
              v-on:updateFournitureIdsForRemoval="updateFournitureIdsForRemoval"
            />
          </b-col>
      </b-row>
   </b-container>
  </div>
</template>

<script>
import Form from './components/Form.vue'
import Inventory from './components/Inventory.vue'

export default {
  name: 'app',
  data () {
    return {
      fournitures: [],
      fournitureIdsForRemoval: [],
      totalVolume: 0
    }
  },
  methods: {
    addNewFourniture(fourniture){
      var newFourniture = {
        id: fourniture.id,
        name: fourniture.name,
        volume: fourniture.volume,
        selectedForDeletion: false
      };
      this.totalVolume += fourniture.volume;
      this.fournitures.push(newFourniture);
    },
    removeFourniture(fournitureId){
      var existingFournitures = this.fournitures;
      for (var i = 0; i < existingFournitures.length; i++){
        if (existingFournitures[i].id === fournitureId) {
          existingFournitures.splice(i, 1);
        }
      }
      this.fournitures = existingFournitures;
      this.setTotalVolume();
    },
    removeFournitures() {
      var existingFournitures = this.fournitures;
      for (var i = 0; i < this.fournitureIdsForRemoval.length; i++){
        var item = this.getItemToDelete(this.fournitureIdsForRemoval[i]);
        var itemIndex = this.fournitures.indexOf(item[0]);
        if (itemIndex >= 0){
          this.fournitures.splice(itemIndex, 1);
        }
      }
      this.fournitureIdsForRemoval = [];
      this.setTotalVolume();
    },
    getItemToDelete(fournitureIdForRemoval){
      return this.fournitures.filter(fourniture => fournitureIdForRemoval == fourniture.id);
    },
    updateFournitureIdsForRemoval(values){
      this.fournitureIdsForRemoval = values;
    },
    setTotalVolume(){
      this.totalVolume = 0;
      for (var i = 0; i < this.fournitures.length; i++) {
        this.totalVolume += this.fournitures[i].volume;
      }
    }
  },
  components: {
    Form,
    Inventory
  }
}
</script>
