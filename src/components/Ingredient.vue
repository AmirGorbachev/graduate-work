<template lang="pug">
  .ingredient(
    @dragstart="dragStart"
    @drag="dragging"
    draggable="true"
    :id="title"
  )
    p {{title}}
</template>

<script>
export default {
  name: 'Ingredient',
  props: {
    title: {
      type: [Number, String],
      requiered: true,
    },
  },
  data() {
    return {}
  },
  methods: {
    dragStart: function (event) {
      event.dataTransfer.setData('Ingredient', event.target.id)
    },
    dragging: function (event) {},
  },
}
</script>

<style scoped lang="scss">
.ingredient {
  background-color: green;
}
</style>
