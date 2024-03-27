<script setup>
  import {ref} from "vue";

  const showModal = ref(false);
  const newNote = ref('');
  const notes = ref([]);

  function getRandomColor() {
    return `hsl(${Math.random() * 360}, 100%, 75%)`;
  }

  const addNote = () => {
    notes.value.push({
      id: Math.floor(Math.random() * 100000000000),
      text: newNote.value,
      date: new Date(),
      backgroundColor: getRandomColor()
    });
    showModal.value = false;
    newNote.value = '';
  }
</script>

<template>
  <main>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <textarea v-model="newNote" name="note" id="note" cols="30" rows="10"></textarea>
        <button @click="addNote">Add Note</button>
        <button class="close" @click="showModal = false">Close</button>
      </div>
    </div>
    <div class="container">
      <header> 
        <h1>Notes</h1>
        <button @click="showModal = true">+</button>
      </header>
      <div class="cards-container">
        <div v-for="note in notes" class="card" :style="{backgroundColor:note.backgroundColor}">
          <p class="maintext">{{ note.text }}</p>
          <p class="date">{{note.date.toLocaleDateString("nl-NL")}}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
  main {
    height: 100vh;
    width: 100vw;
  }
  .overlay {
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: rgba(0,0,0,.77);
    z-index: 10;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .modal {
    width: 750px;
    background-color: var(--color-background);
    border-radius: 10px;
    padding: 30px;
    position: relative;
    display: flex;
    flex-direction: column;
  }
  .modal button {
    padding: 10px 20px;
    font-size: 20px;
    width: 100%;
    background-color: blueviolet;
    border: none;
    color: white;
    cursor: pointer;
    margin-top: 15px;
  }
  .modal .close  {
    background-color: rgb(193,15,15);
    margin-top: 7px;
  }
  .container {
    max-width: 1000px;
    padding: 10px;
    margin: 0 auto;
  }
  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  h1 {
    font-weight: 700;
    margin-bottom: 25px;
    font-size: 75px;
  }
  header button {
    border: none;
    padding: 10px;
    width: 50px;
    height: 50px;
    cursor: pointer;
    background-color: var(--color-text);
    color: var(--color-background);
    font-size: 20px;
    border-radius: 100%;
  }
  .cards-container {
    display: flex;
    flex-wrap: wrap;
  }
  .card {
    width: 250px;
    height: 250px;
    background-color: rgb(237,182,44);
    padding: 10px;
    border-radius: 15px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin: 0 20px 20px 0;
  }
  .date {
    font-size: 12px;
    font-weight: 700;
  }
</style>