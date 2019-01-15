<template>
  <div>
    <b-card>
      <div v-for="fourniture in fournitures">
        <div style="display: flex;justify-content: space-between;">
          <input type="checkbox">
          <div >{{fourniture.name}}</div>
        </div>
      </div>
    </b-card>
  </div>
</template>

<script>
export default {
  props: ["fournitures"],
  methods: {
  }
}
</script>
