<template>

<div class="wrapper">
  <div class="wrapper-content">

    <section>

      <div class="container"> 
  
        <NewMessege v-if="NewMessege" :NewMessege="NewMessege"/> 
        <NewImr v-if="NewImr" :NewImr="NewImr"/>

        <newNote v-model:note="note" v-model:importants="importants" @addNote="AddNote"/>

        <div class="note-header">

          <h1>{{ title }}</h1>

          <search :value="search"  placeholder="Find the note" @search="search = $event"/>

          <icons :grid="grid" @changeGrid="ChangeGrid"/>

        </div>

        <notes :notes="notesFilter" :grid="grid" @remove="removeNote"/>

      </div>

    </section>

  </div>

</div>

</template>

<script>

import NewMessege from '@/components/NewMessege.vue'
import NewImr from '@/components/NewImpr.vue'
import notes from '@/components/ZametkiNovye.vue'
import Search from './components/SearchNote.vue'
import newNote from '@/components/newNote.vue'
import icons from '@/components/IconsChange.vue'

export default {
  name: 'App',
  components: {
    NewMessege,
    newNote,
    NewImr,
    notes,
    Search,
    icons
  },
  data () {
    return {
    title: 'Notes App',
    NewMessege: null,
    NewImr: null,
    grid: true,
    search: '',
    importants: ['Important', 'Normal', 'No matter'],
    note: {
      title:'',
      descr:'',
      impr: ''
    },
    notes: [
      {
        title: 'First note',
        descr: 'Description for first note',
        impr: 'Important',
        date: new Date(Date.now()).toLocaleString()
      },
      {
        title: 'Second note',
        descr: 'Description for second note',
        impr: 'Normal',
        date: new Date(Date.now()).toLocaleString()
      },
      {
        title: 'Third note',
        descr: 'Description for third note',
        impr: 'No matter',
        date: new Date(Date.now()).toLocaleString()
      },
    ]
  }
  },
  computed: {
    notesFilter () {
      let array = this.notes
      let search = this.search

      if (!search) return array //Чтобы поиск не искал пустую строку, т.е. если search равно false
      search = search.trim().toLowerCase() //Избовляем то, что будем искать от пробелов (trim()) и приводим это к нижнему регистру (toLowerCase())

      array = array.filter (function (item) {if (item.title.toLowerCase().indexOf(search) !== -1) 
      return item})

      return array
    }
  },
  methods: {
    AddNote () {
      let {title, descr, impr} = this.note

      if (title === '') {

        this.NewMessege = 'Wrong note'
        return false

      } 
      if (impr === '') {

      this.NewImr = 'Choose the importance of note'
      return false

      }
      this.notes.push({
        title,
        descr,
        impr,
        date: new Date(Date.now()).toLocaleString()
      })
      this.NewMessege = null
      this.NewImr = null
      this.note.title = ''
      this.note.descr = ''
      this.note.impr = ''
    },
    removeNote (index) {
      this.notes.splice(index, 1)
    },
    СhangeNote () {
        let {title} = this.note

        this.notes.splice({
          title
        })
        this.note.title = ''
    },
    ChangeGrid () {
      this.grid = !this.grid
    }
  }
}
</script>

<style>

</style>

//Сообщение для проверки коммита