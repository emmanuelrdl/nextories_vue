<template>
  <div>
    <b-form @submit="onSubmit">
      <b-row>
        <b-col cols="8">
          <b-form-group >
            <b-form-input
              type="text"
              v-model="name"
              @change="formChange"
              required
              placeholder="Nom du meuble">
            </b-form-input>
          </b-form-group>
          <b-form-group >
            <b-form-input
              v-model="length"
              required
              @change="formChange"
              placeholder="Longueur (cm)">
            </b-form-input>
          </b-form-group>
          <b-form-group >
            <b-form-input
              v-model="width"
              required
              @change="formChange"
              placeholder="Largeur (cm)">
            </b-form-input>
          </b-form-group>
          <b-form-group >
            <b-form-input
              v-model="height"
              required
              @change="formChange"
              placeholder="Hauteur (cm)">
            </b-form-input>
          </b-form-group>
        </b-col>
        <b-col cols="4">
          <div class="single-volume-card">
            <h5>Volume (m3):</h5>
            <br>
            <h5>{{volume}}</h5>
          </div>
          <b-button type="submit" variant="primary">AJOUTER</b-button>
        </b-col>
      </b-row>
    </b-form>
  </div>
</template>

<script>
export default {
  props: ["fournitures"],
  data () {
    return {
      id: null,
      name: null,
      height: null,
      width: null,
      length: null,
      volume: null
    }
  },
  methods: {
    onSubmit (evt) {
      evt.preventDefault();
      this.volume = this.getVolume();
      this.id     = this.fakeId();
      if (this.formIsValid()) this.$emit('newFourniture', this.$data);
    },
    getVolume(form){
      var height   = this.height;
      var width    = this.width;
      var length   = this.length;
      var volInCm  = parseInt(height) * parseInt(width) * parseInt(length);
      return volInCm/100;
    },
    formIsValid(){
      if (this.completedForm() && this.validTypes()){
        return true;
      }
      return false;
    },
    validTypes(){
      var props = ['height', 'width', 'length'];
      for (var i = 0; i < 3; i++){
        if (!this[props[i]].match(/[1-9]/g)) {
          alert('cannot calculate volume');
          return false;
        }
      }
      return true;
    },
    completedForm(){
      return this.name && this.height && this.width && this.length;
    },
    formChange(){
      if (this.formIsValid()) {
        this.volume = this.getVolume();
      }
    },
    fakeId(){
      if (this.fournitures.length === 0){
        return 1;
      } else {
        return this.fournitures[this.fournitures.length -1].id + 1;
      }
    }
  }
}
</script>
