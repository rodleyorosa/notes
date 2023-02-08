<template>
  <div class="my-10">
    <Modal
    v-if="isModalOpened"
    @cancelModal="cancelModal()"
    @addNote="addNote" />
    <div class="max-w-md m-auto flex justify-between items-center">
      <h1 class="text-4xl font-bold">NOTES</h1>
      <button
      @click="isModalOpened = true"
      class="bg-gray-800 text-white w-10 h-10 rounded-full hover:bg-gray-900">+</button>
    </div>
    <div class="max-w-4xl m-auto py-10 flex flex-wrap justify-around">
      <div v-for="note in notes" :key="note">
        <div class="w-56 h-56 bg-orange-300 p-2.5 rounded-xl flex flex-col justify-between mr-5 mb-5">
          <p class="">{{ note.text }}</p>
          <p class="text-xs font-bold">{{ note.date }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Modal from '../src/components/Modal.vue'

const isModalOpened = ref(false)
const notes = ref([])

function cancelModal() {
  isModalOpened.value = false
}

function addNote(newNote) {
  let objectDate = new Date();
  let day = objectDate.getDate();
  let month = objectDate.getMonth();
  let year = objectDate.getFullYear();
  let date = day + '/' + month + '/' + year

  notes.value.push({
    id: Math.floor(Math.random() * 1000000),
    text: newNote,
    date: date,
    // bgColor: ,
  })

  isModalOpened.value = false
}

</script>