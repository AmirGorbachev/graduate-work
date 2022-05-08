<template lang="pug">
  div
    .field
      .field__list
        .field__item.cell(v-for='(item, index) in field')
          .cell__wrapper(:class='getCellClass(item.id)' ref='cell' @click='pickCell(item)')
            p(v-html='item.label')
            p {{item.value}}

    pre {{availableMoveListId}}
</template>

<script>
export default {
  name: 'Field',
  components: {},
  data() {
    return {
      field: [
        { id: 0, value: '', label: '' },
        { id: 1, value: '', label: '' },
        { id: 2, value: '', label: '' },
        { id: 3, value: '', label: '' },
        { id: 4, value: '', label: '' },
        { id: 5, value: '', label: '' },
        { id: 6, value: '', label: '' },
        { id: 7, value: '', label: '' },

        { id: 8, value: '', label: '' },
        { id: 9, value: '', label: '' },
        { id: 10, value: '', label: '' },
        { id: 11, value: '', label: '' },
        { id: 12, value: '', label: '' },
        { id: 13, value: '', label: '' },
        { id: 14, value: '', label: '' },
        { id: 15, value: '', label: '' },

        { id: 16, value: '', label: '' },
        { id: 17, value: '', label: '' },
        { id: 18, value: '', label: '' },
        { id: 19, value: '', label: '' },
        { id: 20, value: '', label: '' },
        { id: 21, value: '', label: '' },
        { id: 22, value: '', label: '' },
        { id: 23, value: '', label: '' },

        { id: 24, value: '', label: '' },
        { id: 25, value: '', label: '' },
        { id: 26, value: '', label: '' },
        { id: 27, value: '', label: '' },
        { id: 28, value: '', label: '' },
        { id: 29, value: '', label: '' },
        { id: 30, value: '', label: '' },
        { id: 31, value: '', label: '' },

        { id: 32, value: '', label: '' },
        { id: 33, value: '', label: '' },
        { id: 34, value: '', label: '' },
        { id: 35, value: '', label: '' },
        { id: 36, value: '', label: '' },
        { id: 37, value: '', label: '' },
        { id: 38, value: '', label: '' },
        { id: 39, value: '', label: '' },

        { id: 40, value: '', label: '' },
        { id: 41, value: '', label: '' },
        { id: 42, value: '', label: '' },
        { id: 43, value: '', label: '' },
        { id: 44, value: '', label: '' },
        { id: 45, value: '', label: '' },
        { id: 46, value: '', label: '' },
        { id: 47, value: '', label: '' },

        { id: 48, value: 'pawn', label: '&#9817;', team: true, moved: false },
        { id: 49, value: 'pawn', label: '&#9817;', team: true, moved: false },
        { id: 50, value: 'pawn', label: '&#9817;', team: true, moved: false },
        { id: 51, value: 'pawn', label: '&#9817;', team: true, moved: false },
        { id: 52, value: 'pawn', label: '&#9817;', team: true, moved: false },
        { id: 53, value: 'pawn', label: '&#9817;', team: true, moved: false },
        { id: 54, value: 'pawn', label: '&#9817;', team: true, moved: false },
        { id: 55, value: 'pawn', label: '&#9817;', team: true, moved: false },

        { id: 56, value: 'rook', label: '&#9814;', team: true, moved: false },
        {
          id: 57,
          value: 'knight',
          label: '&#9816;',
          team: true,
          moved: false,
        },
        {
          id: 58,
          value: 'bishop',
          label: '&#9815;',
          team: true,
          moved: false,
        },
        {
          id: 59,
          value: 'queen',
          label: '&#9813;',
          team: true,
          moved: false,
        },
        { id: 60, value: 'king', label: '&#9812;', team: true, moved: false },
        {
          id: 61,
          value: 'bishop',
          label: '&#9815;',
          team: true,
          moved: false,
        },
        {
          id: 62,
          value: 'knight',
          label: '&#9816;',
          team: true,
          moved: false,
        },
        { id: 63, value: 'rook', label: '&#9814;', team: true, moved: false },
      ],
      activeCell: {},
    }
  },
  mounted() {},
  methods: {
    getCellClass(id) {
      if (id == this.activeCell?.id) {
        return 'cell__wrapper_active'
      }

      if (this.availableMoveListId.includes(id)) {
        return 'cell__wrapper_pos-move'
      }
    },
    pickCell(cell) {
      if (!this.activeCell?.id || !this.activeCell.value) {
        this.activeCell = cell

        return
      }

      this.isAvailableMove(this.activeCell, cell)
        ? this.move(cell)
        : (this.activeCell = cell)

      // const cell = this.$refs.cell[id]
    },
    isAvailableMove(cell, newCell) {
      if (!cell.value) {
        return false
      }

      if (this.availableMoveListId.includes(newCell.id)) {
        return true
      }

      return false
    },
    move(cell) {
      cell.label = this.activeCell.label
      cell.value = this.activeCell.value
      cell.team = this.activeCell.team
      cell.moved = true

      this.activeCell.label = ''
      this.activeCell.value = ''
      this.activeCell.team = ''
      this.activeCell.moved = ''

      this.activeCell = {}
    },
  },
  computed: {
    availableMoveListId() {
      let list = []

      if (this.activeCell.value == 'pawn') {
        list.push(this.activeCell.id - 8)

        if (!this.activeCell?.moved) {
          list.push(this.activeCell.id - 16)
        }
      }

      return list
    },
  },
  watch: {},
}
</script>

<style scoped lang="scss">
$item: 100px;

.field {
  display: flex;
  justify-content: center;
  align-items: center;

  &__list {
    margin: 5px;
    display: flex;
    flex-wrap: wrap;
    width: calc($item * 8);
    border: 1px solid black;
  }

  &__item {
  }
}

.cell {
  &__wrapper {
    display: flex;
    justify-content: center;
    align-items: center;
    height: $item;
    width: $item;
    background: #fdd9b5;
    transition-duration: 0.2s;
    transition-timing-function: ease-in;
    cursor: pointer;
    border: 1px solid black;
    box-sizing: border-box;

    &:hover {
      background: darken(#fdd9b5, 10%);
    }

    &_active {
      background: darken(#fdd9b5, 10%);
    }

    &_pos-move {
      background: lighten(#fdd9b5, 5%);
    }

    p {
      font-size: 24px;
    }
  }
}
</style>
