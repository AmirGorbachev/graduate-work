<template>
  <div id="app">
    <p>Drag the p element back and forth between the two rectangles:</p>
    <div class="droptarget" v-on:drop="drop" v-on:dragover="allowDrop">
      <p
        @dragstart="dragStart"
        @drag="dragging"
        draggable="true"
        id="dragtarget"
      >
        Drag me!
      </p>
    </div>

    <div class="droptarget" @drop="drop" @dragover="allowDrop"></div>

    <p id="demo"></p>
  </div>
</template>

<script>
export default {
  name: 'home',
  data() {
    return {}
  },
  mounted() {},
  methods: {
    dragStart: function (event) {
      event.dataTransfer.setData('Text', event.target.id)
    },
    dragging: function (event) {
      document.getElementById('demo').innerHTML =
        'The p element is being dragged'
    },
    allowDrop: function (event) {
      event.preventDefault()
    },
    drop: function (event) {
      event.preventDefault()
      var data = event.dataTransfer.getData('Text')
      event.target.appendChild(document.getElementById(data))
      document.getElementById('demo').innerHTML = 'The p element was dropped'
    },
  },
  watch: {},
}
</script>

<style scoped lang="scss">
.droptarget {
  width: 100px;
  height: 35px;
  margin: 15px;
  padding: 10px;
  border: 1px solid #aaaaaa;
}
</style>
