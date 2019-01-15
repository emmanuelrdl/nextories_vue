<template>
  <div id="app">
    <b-container class="bv-example-row">
      <b-row>
          <b-col cols="7">
            <Form v-on:newFourniture="addNewFourniture"/>
          </b-col>
          <b-col cols="5"></b-col>
      </b-row>
      <b-row>
          <b-col cols="12">
            <div style="display: flex;justify-content: space-between;">
              <div class="pull-left">Inventaire</div>
              <div>Volume Total: {{totalVolume}}</div>
            </div>
            <Inventory
                      v-bind:fournitures="fournitures"/>
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
      totalVolume: 0
    }
  },
  methods: {
    addNewFourniture(fourniture){
      var newFourniture = {
        name: fourniture.name,
        volume: fourniture.volume
      };
      this.totalVolume += fourniture.volume;
      this.fournitures.push(newFourniture);
    }
  },
  components: {
    Form,
    Inventory
  }
}
</script>
