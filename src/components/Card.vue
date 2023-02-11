<template>
  <div
    class="w-56 h-56 p-2.5 overflow-hidden rounded-xl flex flex-col justify-between mr-5 mb-5"
    :style="{ backgroundColor: note.bgColor }"
  >
  <ModalDelete
    v-if="isDeleteModalOpened"
    @cancelDelete="isDeleteModalOpened = !isDeleteModalOpened"
    :id="id"
    @deleteNote="deleteNote" />
    <div>
      <div class="flex justify-between items-center">
        <div>
          <h2
          v-if="!editTitle"
          @click.prevent="editTitle = !editTitle"
          class="font-bold">{{ note.newNote.title }}</h2>
          <input type="text"
          v-if="editTitle"
          v-model="note.newNote.title"
          @keydown.enter="$emit('editTitle', [id, note.newNote.title])"
          class="outline-none font-bold w-full"
          :style="{backgroundColor: note.bgColor}">
        </div>
        <div class="space-x-3 flex">
         <button
           @click.prevent="isDeleteModalOpened = !isDeleteModalOpened">
           <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="currentColor" class="bi bi-trash3" viewBox="0 0 16 16">
             <path d="M6.5 1h3a.5.5 0 0 1 .5.5v1H6v-1a.5.5 0 0 1 .5-.5ZM11 2.5v-1A1.5 1.5 0 0 0 9.5 0h-3A1.5 1.5 0 0 0 5 1.5v1H2.506a.58.58 0 0 0-.01 0H1.5a.5.5 0 0 0 0 1h.538l.853 10.66A2 2 0 0 0 4.885 16h6.23a2 2 0 0 0 1.994-1.84l.853-10.66h.538a.5.5 0 0 0 0-1h-.995a.59.59 0 0 0-.01 0H11Zm1.958 1-.846 10.58a1 1 0 0 1-.997.92h-6.23a1 1 0 0 1-.997-.92L3.042 3.5h9.916Zm-7.487 1a.5.5 0 0 1 .528.47l.5 8.5a.5.5 0 0 1-.998.06L5 5.03a.5.5 0 0 1 .47-.53Zm5.058 0a.5.5 0 0 1 .47.53l-.5 8.5a.5.5 0 1 1-.998-.06l.5-8.5a.5.5 0 0 1 .528-.47ZM8 4.5a.5.5 0 0 1 .5.5v8.5a.5.5 0 0 1-1 0V5a.5.5 0 0 1 .5-.5Z" />
           </svg>
         </button>
        </div>
      </div>
      <p v-if="!isEditOpened"
      @click="isEditOpened = !isEditOpened"
      class="">{{ note.newNote.msg }}</p>
      <input v-if="isEditOpened"
      class="outline-none w-full"
      @keydown.enter="$emit('editNote', [id, note.newNote.msg])"
      :style="{backgroundColor: note.bgColor}"
      v-model="note.newNote.msg"
      name="" id="">
    </div>
    <p class="text-xs font-bold">{{ note.date }}</p>
  </div>
</template>

<script setup>
import ModalDelete from './ModalDelete.vue'
import { ref } from 'vue'

const props = defineProps([
 'note',
 'isDeleteModalOpened',
 'id'
])

const emit = defineEmits([
 'deleteNote',
 'editNote',
 'editTitle'
])

const isEditOpened = ref(false)
const editTitle = ref(false)

function deleteNote(id) {
 emit('deleteNote', id)
}

</script>