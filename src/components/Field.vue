<template lang="pug">
  .field
    .field__wrapper
      .field__list(v-for='list in field')
        .field__item.cell(v-for='item in list')
          .cell__wrapper(ref='cell' @click='initCharacter(item.id)')
            p(v-if='item.id == activeCell') &#9822;
            p(v-if='item.value == `tree`') &#127794;
            p(v-if='item.value == `pig`') &#128022;
            p {{item.id}}
</template>

<script>
export default {
  name: 'Field',
  components: {},
  data() {
    return {
      field: [
        [{ id: 0, value: 'tree', background: 'forest' }, { id: 1 }, { id: 2 }],
        [{ id: 3 }, { id: 4, value: 'pig', background: 'forest'  }, { id: 5 }],
        [{ id: 6 }, { id: 7 }, { id: 8 }],
      ],
      activeCell: 0,
    }
  },
  mounted() {},
  methods: {
    initCharacter(id) {
      const cell = this.$refs.cell[id]
      console.log(cell)

      this.activeCell = id
    },
  },
  watch: {},
}
</script>

<style scoped lang="scss">
$gap: 2px;

.field {
  display: flex;
  justify-content: center;
  align-items: center;

  &__wrapper {
    padding: 5px;
    display: flex;
    flex-direction: column;
    gap: $gap;
  }

  &__list {
    display: flex;
    gap: $gap;
  }

  &__item {
  }
}

.cell {
  &__wrapper {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100px;
    width: 100px;
    background: #fdd9b5;
    transition-duration: 0.2s;
    transition-timing-function: ease-in;
    cursor: pointer;

    &:hover {
      background: darken(#fdd9b5, 10%);
    }
  }
}
</style>
