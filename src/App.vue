<template>
  <div class="my-10">
    <Modal
    v-if="isModalOpened"
    @cancelModal="cancelModal()"
    @addNote="addNote" />
    <ModalDelete
    v-if="isDeleteModalOpened"
    @deleteNote="deleteNote"
    @cancelDelete="isDeleteModalOpened = false" />
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
        <div
        class="w-56 h-56 p-2.5 overflow-hidden rounded-xl flex flex-col justify-between mr-5 mb-5"
        :style="{backgroundColor: note.bgColor}">
          <div>
            <div class="flex justify-between items-center">
              <h2 class="font-bold">{{ note.newNote.title }}</h2>
              <button @click.prevent="isDeleteModalOpened = true">
                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-trash3" viewBox="0 0 16 16">
                  <path d="M6.5 1h3a.5.5 0 0 1 .5.5v1H6v-1a.5.5 0 0 1 .5-.5ZM11 2.5v-1A1.5 1.5 0 0 0 9.5 0h-3A1.5 1.5 0 0 0 5 1.5v1H2.506a.58.58 0 0 0-.01 0H1.5a.5.5 0 0 0 0 1h.538l.853 10.66A2 2 0 0 0 4.885 16h6.23a2 2 0 0 0 1.994-1.84l.853-10.66h.538a.5.5 0 0 0 0-1h-.995a.59.59 0 0 0-.01 0H11Zm1.958 1-.846 10.58a1 1 0 0 1-.997.92h-6.23a1 1 0 0 1-.997-.92L3.042 3.5h9.916Zm-7.487 1a.5.5 0 0 1 .528.47l.5 8.5a.5.5 0 0 1-.998.06L5 5.03a.5.5 0 0 1 .47-.53Zm5.058 0a.5.5 0 0 1 .47.53l-.5 8.5a.5.5 0 1 1-.998-.06l.5-8.5a.5.5 0 0 1 .528-.47ZM8 4.5a.5.5 0 0 1 .5.5v8.5a.5.5 0 0 1-1 0V5a.5.5 0 0 1 .5-.5Z"/>
                </svg>
              </button>
            </div>
            <p class="">{{ note.newNote.msg }}</p>
          </div>
          <p class="text-xs font-bold">{{ note.date }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Modal from './components/Modal.vue'
import ModalDelete from './components/ModalDelete.vue'

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

function addNote(title) {
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

  notes.value.push({
    // id: Math.floor(Math.random() * 1000000),
    newNote: title,
    date: date,
    bgColor: getRandomColor(),
  })
  console.log(notes.value)

  isModalOpened.value = false
}

function deleteNote(id) {
    // notes.value.splice(id, 1)
    // isDeleteModalOpened.value = false
    console.log(id)
}

</script>