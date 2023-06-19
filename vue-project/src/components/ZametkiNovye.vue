<template>

<div class="notes">

    <noteUnit class="note-unit" v-for="(note, index) in notes" :note="note" :key="index" @remove="remove" :grid="grid"/>

  </div>

</template>

<script>

import noteUnit from '@/components/NoteUnit.vue'

export default {
  components: {
    noteUnit
  },
  data: () => {
    return {
      changeN: true,
      curIndex: undefined
    }
  },
    props: {
        notes: {
          type: Array,
          required: true
        },
        grid: {
          type: Boolean,
          required: true
        }
    },
    methods: {
        remove (index) {
            this.$emit ('remove', index)
        }
}
}


</script>

<style lang="scss">

.note-unit {
  &.full {
    justify-content: center;
    p {
      margin-right: 16px;
      &:last-child {
        margin-right: 0;
      }
    }
  }
}

.notes {
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-wrap: wrap;
    padding: 40px 0;
}


</style>

