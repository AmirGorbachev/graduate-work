<template lang="pug">
.table
  .table__wrapper
    .table__area(
      @drop="drop"
      @dragover="allowDrop"
    )
</template>

<script>
export default {
  name: 'Table',
  props: {
    msg: String,
  },
  data() {
    return {
      action: '',
    }
  },
  methods: {
    allowDrop: function (event) {
      event.preventDefault()
    },
    drop: function (event) {
      event.preventDefault()
      var data = event.dataTransfer.getData('Ingredient')
      event.target.appendChild(document.getElementById(data))
    },
  },
}
</script>

<style scoped lang="scss">
.table {
  height: 350px;
  width: 350px;

  &__wrapper {
    height: 100%;
    width: 100%;
  }

  &__area {
    height: 100%;
    width: 100%;
    background-color: yellow;
  }
}
</style>
