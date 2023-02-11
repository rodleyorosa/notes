<template>
  <div class="my-10">
    <Modal
    v-if="isModalOpened"
    @cancelModal="cancelModal()"
    @addNote="addNote" />
    <div class="max-w-md m-auto">
      <div class="flex justify-between items-center">
        <h1 class="text-4xl font-bold">NOTES</h1>
        <button
        @click="openModal()"
        class="bg-gray-800 text-white w-10 h-10 rounded-full hover:bg-gray-900">+</button>
      </div>
      <p class="text-sm">* Done with emit</p>
    </div>
    <div class="max-w-6xl m-auto py-10 flex flex-wrap justify-around">
      <div v-for="(note, id) in notes" :key="id">
        <Card
        :note="note"
        :isDeleteModalOpened="isDeleteModalOpened"
        :id="id"
        @deleteNote="deleteNote"
        @editNote="editNote"
        @editTitle="editTitle" />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Modal from './components/Modal.vue'
import Card from './components/Card.vue'

const isModalOpened = ref(false)
const notes = ref([])
const textarea = ref(null)
const isDeleteModalOpened = ref(false)

function getRandomColor() {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
}

function openModal() {
  isModalOpened.value = true
}

function cancelModal() {
  isModalOpened.value = false
}

function addNote(note) {
  let objectDate = new Date();
  let day = objectDate.getDate();
  if (day < 10) {
    day = '0' + day
  }
  let month = objectDate.getMonth() + 1;
  if (month < 10) {
    month = '0' + month
  }
  let year = objectDate.getFullYear();
  let date = day + '/' + month + '/' + year

  if(!note.title) {
    note.title = 'no-title'
  }

  notes.value.push({
    // id: Math.floor(Math.random() * 1000000),
    newNote: note,
    date: date,
    bgColor: getRandomColor(),
  })

  isModalOpened.value = false
}

function deleteNote(id) {
    notes.value.splice(id, 1)
    isDeleteModalOpened.value = false
}

function editNote(param) {
  // param[0] = id
  // param[1] = msg
  notes.value[param[0]].newNote.msg = param[1]
}

function editTitle(param) {
  notes.value[param[0]].newNote.title = param[1]
}

</script>