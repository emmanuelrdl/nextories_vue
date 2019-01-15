<template>
  <div>
    <b-form @submit="onSubmit">
      <b-row>
        <b-col cols="8">
          <b-form-group >
            <b-form-input
                          type="text"
                          v-model="form.name"
                          @change="formChange"
                          required
                          placeholder="Nom du meuble">
            </b-form-input>
          </b-form-group>
          <b-form-group >
            <b-form-input
                          v-model="form.length"
                          required
                          @change="formChange"
                          placeholder="Longueur (cm)">
            </b-form-input>
          </b-form-group>
          <b-form-group >
            <b-form-input
                          v-model="form.width"
                          required
                          @change="formChange"
                          placeholder="Largeur (cm)">
            </b-form-input>
          </b-form-group>
          <b-form-group >
            <b-form-input
                          v-model="form.height"
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
  data () {
    return {
      form: {
        name: null,
        height: null,
        width: null,
        length: null,
      },
      volume: null,
    }
  },
  methods: {
    onSubmit (evt) {
      evt.preventDefault();
      this.volume = this.getVolume(this.form);
    },
    getVolume(form){
      var height = form.height
      var width  = form.width
      var length = form.length
      var volInCm  = parseInt(height) * parseInt(width) * parseInt(length)
      return volInCm/100
    },
    formIsValid(){
      return this.form.height && this.form.width && this.form.length
    },
    formChange(){
      if (this.formIsValid()) {
        this.volume = this.getVolume(this.form);
      }
    }
  }
}
</script>
