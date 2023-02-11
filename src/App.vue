<script setup>
  import { ref } from 'vue';

  const showModel = ref(false);
  const newNote = ref('');
  const notes = ref([]);
  const options = {month: 'long', day: 'numeric', year: 'long'}

  function getRandomColor() {
    var letters = '0123456789ABCDEF'.split('');
    var color = '#';
    for (var i = 0; i < 6; i++ ) {
        color += letters[Math.floor(Math.random() * 16)];
    }
    return color;
}

  const addNote = () => {
    notes.value.push({
      id: Math.floor(Math.random() * 1000000),
      text: newNote.value,
      date: new Date(MM/DD/YYYY),
      backgroundColor: getRandomColor(),
      options,
    });
    showModel.value = false;
    newNote.value = '';
  }
</script>

<template>
  <main>
    <div v-if="showModel" class="overlay">
      <div class="model">
        <textarea name="note"  v-model='newNote' id="note" cols="30" rows="10"></textarea>
        <button class="add-btn" showModel="true" @click="addNote()">Add Note</button>
        <button class="close-btn" @click="showModel = false">Close</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes </h1>
        <button @click="showModel = true">+</button>
      </header>
      <div class="cards-container">
        <div v-for="note in notes" class="card" :style="{backgroundColor: note.backgroundColor}">
          <p class="main-text">{{ note.text }}</p>
          <p class="date">{{ note.date.toLocalDateString('en-US') }}</p>  
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
    font-weight: bold;
    margin-bottom: 25px;
    font-size: 75px;
  }

  header button {
    border: none;
    padding: 10px;
    width: 50px;
    height: 50px;
    cursor: pointer;
    background-color: rgb(21, 20, 20);
    border-radius: 100%;
    color: white;
    font-size: 20px;
  }

  .card {
    width: 225px;
    height: 225px;
    background-color: rgb(237, 182, 44);
    padding: 10px;
    border-radius: 15px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-right: 20px;
    margin-bottom: 20px;
  }
  .date {
    font-size: 12.5px;
    font-weight: bold;
  }

  .cards-container {
    display: flex;
    flex-wrap: wrap;
  }

  .overlay {
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, .77);
    z-index: 10;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .model {
    width: 750px;
    background-color: white;
    border-radius: 10px;
    padding: 30px;
    position: relative;
    display: flex;
    flex-direction: column;
  }

  .model button {
    padding: 10px 20px;
    font-size: 20px;
    width: 100%;
    background-color: blueviolet;
    border: none;
    color: white;
    cursor: pointer;
    margin-top: 15px;
  }

  .model .close-btn {
    background-color: rgb(193, 20, 20);
    margin-top: 15px;
  }
</style>