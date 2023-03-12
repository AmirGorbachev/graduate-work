<template lang="pug">
  .kitchen
    .kitchen__head
      .kitchen__bowls
        Bowl(:items='bowl1')
        Bowl(:items='bowl2')
        Bowl(:items='bowl3')
    .kitchen__content
      .kitchen__table
        Table
    .kitchen__footer
</template>

<script>
import Table from '@/components/Table'
import Bowl from '@/components/Bowl'

export default {
  name: 'Kitchen',
  components: {
    Table,
    Bowl,
  },
  data() {
    return {
      bowl1: [
        {
          id: 1,
          title: 'Tomato',
        },
        {
          id: 2,
          title: 'Tomato',
        },
        {
          id: 3,
          title: 'Tomato',
        },
      ],
      bowl2: [
        {
          id: 1,
          title: 'Cucumber',
        },
        {
          id: 2,
          title: 'Cucumber',
        },
        {
          id: 3,
          title: 'Cucumber',
        },
      ],
      bowl3: [
        {
          id: 1,
          title: 'Meat',
        },
        {
          id: 2,
          title: 'Meat',
        },
        {
          id: 3,
          title: 'Meat',
        },
      ],
    }
  },
}
</script>

<style scoped lang="scss">
.kitchen {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  &__head {
  }

  &__bowls {
    display: flex;
    gap: 20px;
  }

  &__content {
    display: flex;
    gap: 20px;
    align-items: flex-end;
  }

  &__table {
    margin-top: 50px;
  }

  &__footer {
  }
}
</style>
