<template lang="pug">
  div
    .field
      .field__list
        .field__item.cell(v-for='(item, index) in field')
          .cell__wrapper(:class='getCellClass(index)' ref='cell' @click='pickCell(item, index)')
            p(v-if='item.value == `pawn` && item.team == 1' v-html='`&#9817;`')
            p(v-else-if='item.value == `pawn` && item.team == 2' v-html='`&#9823;`')
            p(v-else-if ='item.value == `rook` && item.team == 1' v-html='`&#9814;`')
            p(v-else-if ='item.value == `rook` && item.team == 2' v-html='`&#9820;`')
            p(v-else-if ='item.value == `knight` && item.team == 1' v-html='`&#9816;`')
            p(v-else-if ='item.value == `knight` && item.team == 2' v-html='`&#9822;`')
            p(v-else-if ='item.value == `bishop` && item.team == 1' v-html='`&#9815;`')
            p(v-else-if ='item.value == `bishop` && item.team == 2' v-html='`&#9821;`')
            p(v-else-if ='item.value == `queen` && item.team == 1' v-html='`&#9813;`')
            p(v-else-if ='item.value == `queen` && item.team == 2' v-html='`&#9819;`')
            p(v-else-if ='item.value == `king` && item.team == 1' v-html='`&#9812;`')
            p(v-else-if ='item.value == `king` && item.team == 2' v-html='`&#9818;`')

    pre availableMoveListId: {{availableMoveListId}}
</template>

<script>
export default {
  name: 'Field',
  components: {},
  data() {
    return {
      field: [
        {},
        {},
        {},
        {},
        {},
        {},
        {},
        {},

        { value: 'pawn', team: 2, moved: false },
        { value: 'pawn', team: 2, moved: false },
        { value: 'pawn', team: 2, moved: false },
        { value: 'pawn', team: 2, moved: false },
        { value: 'pawn', team: 2, moved: false },
        { value: 'pawn', team: 2, moved: false },
        { value: 'pawn', team: 2, moved: false },
        { value: 'pawn', team: 2, moved: false },

        {},
        {},
        {},
        {},
        {},
        {},
        {},
        {},

        {},
        {},
        {},
        {},
        {},
        {},
        {},
        {},

        {},
        {},
        {},
        {},
        {},
        {},
        {},
        {},

        {},
        {},
        { value: 'pawn', team: 2, moved: false },
        {},
        {},
        { value: 'pawn', team: 1, moved: false },
        { value: '' },
        { value: '' },

        { value: 'pawn', team: 1, moved: false },
        { value: 'pawn', team: 1, moved: false },
        { value: 'pawn', team: 1, moved: false },
        { value: 'pawn', team: 1, moved: false },
        { value: 'pawn', team: 1, moved: false },
        { value: 'pawn', team: 1, moved: false },
        { value: 'pawn', team: 1, moved: false },
        { value: 'pawn', team: 1, moved: false },

        { value: 'rook', team: 1, moved: false },
        {
          value: 'knight',
          team: 1,
          moved: false,
        },
        {
          value: 'bishop',
          team: 1,
          moved: false,
        },
        {
          value: 'queen',
          team: 1,
          moved: false,
        },
        { value: 'king', team: 1, moved: false },
        {
          value: 'bishop',
          team: 1,
          moved: false,
        },
        {
          value: 'knight',
          team: 1,
          moved: false,
        },
        { value: 'rook', team: 1, moved: false },
      ],
      activeCellId: null,
      activeCell: {},
    }
  },
  mounted() {},
  methods: {
    getCellClass(id) {
      if (id == this.activeCellId) {
        return 'cell__wrapper_active'
      }

      if (this.availableMoveListId.includes(id)) {
        return 'cell__wrapper_pos-move'
      }
    },
    pickCell(cell, id) {
      if (
        !this.activeCellId ||
        !this.activeCell.value ||
        !this.isAvailableMove(this.activeCell, id)
      ) {
        this.activeCellId = id
        this.activeCell = cell

        return
      }

      this.move(cell)
    },
    isAvailableMove(cell, newCellId) {
      if (!cell.value) {
        return false
      }

      if (this.availableMoveListId.includes(newCellId)) {
        return true
      }

      return false
    },
    move(cell) {
      cell.label = this.activeCell.label
      cell.value = this.activeCell.value
      cell.team = this.activeCell.team
      cell.moved = true

      this.activeCellId = null

      this.activeCell.label = ''
      this.activeCell.value = ''
      this.activeCell.team = ''
      this.activeCell.moved = ''
    },
  },
  computed: {
    availableMoveListId() {
      if (!this.activeCellId) {
        return []
      }

      let list = []

      if (this.activeCell.value == 'pawn') {
        if (!this.field[this.activeCellId - 8].value) {
          list.push(this.activeCellId - 8)
        }

        if (
          !this.activeCell?.moved &&
          !this.field[this.activeCellId - 16].value &&
          !this.field[this.activeCellId - 8].value
        ) {
          list.push(this.activeCellId - 16)
        }

        if (
          typeof this.field[this.activeCellId - 7]?.team == 'number' &&
          this.activeCell?.team != this.field[this.activeCellId - 7]?.team
        ) {
          list.push(this.activeCellId - 7)
        }

        if (
          typeof this.field[this.activeCellId - 9]?.team == 'number' &&
          this.activeCell?.team != this.field[this.activeCellId - 9]?.team
        ) {
          list.push(this.activeCellId - 9)
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
      background: darken(#fdd9b5, 15%);
    }

    &_pos-move {
      background: lighten(#fdd9b5, 10%);
    }

    p {
      font-size: 64px;
    }
  }
}
</style>
