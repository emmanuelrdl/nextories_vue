<template>
  <div>
    <b-card>
      <div v-for="fourniture in fournitures">
        <div style="display: flex;justify-content: space-between;">
          <input type="checkbox">
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
  methods: {
    removeFourniture(fourniture){
      this.$emit("removeFourniture", fourniture.id)
    }
  }
}
</script>
