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
          <div class="volume-card">
            Volume (m3):
            <br>
            {{volume}}
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
      volume: null,
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
      return this.name && this.height && this.width && this.length;
    },
    formChange(){
      if (this.formIsValid()) {
        this.volume = this.getVolume();
      }
    },
    fakeId(){
      if (this.fournitures.length === 0){
        return 1
      } else {
        return this.fournitures[this.fournitures.length -1].id + 1
      }
    }
  }
}
</script>
