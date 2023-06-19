<template>

<div class="new-note">

    <label>Title</label> 
    <input type="text" v-model="note.title"> 

    <label>Importance</label>
    <select v-model="note.impr">
          <option v-for="important in importants" :key="important.index">{{ important }}</option>
      </select>

    <label>Description</label> 
    <textarea v-model="note.descr"></textarea>

    <button class="btn btnPrimary" @click="addNote">New note</button>

</div>

</template>

<script>
export default {
    props: {
    importants: {
      type: Array,
      required: true
    },
    impr:{
      type: String,
      required: true   
    },
    note: {
      type: String,
      required: true
    },
    title: {
        type: String,
        required: true
    },
    descr: {
        type: String,
        required: true
    }
    },
    methods: {
    addNote () {
      this.$emit('addNote', this.note)
    },
    changeTitle () {
      this.$emit('changeTitle', event.target.this.title)
    }
    }
}

</script>

<style scoped>

.new-note {
  text-align: center;
}

</style>