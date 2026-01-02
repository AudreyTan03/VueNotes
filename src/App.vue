<template>
<main>
  <!-- v-if and show yung show = div overlay makikita sa inspect  then v-if reremove ung html element render lang if need, yung show papakita talga lahat-->
  <div v-if="showModal" class="overlay">      <!-- bali v-if showModal = if true papakita lahat till close button kung hanggang saan div -->
      <div class="modal">
    <textarea v-model="newNote" name="note" id="note" cols="30" rows="10"></textarea>
      <button @click="addNote">Add Note</button>
      <button @click="showModal = !showModal">Close</button>   <!-- since naka true din ung close pag naka false yan pwede na mag close or baliktaran ng showmodal -->
    </div>       
  </div>
    <div class="container">
      <header>
        <h1> Notes </h1>
        <button @click="showModal = !showModal">+</button>
      </header>
      <div class="cards-container">
        <div v-for="note in notes" class="card" :style="{backgroundColor: note.backgroundColor}" :key="note.id">  <!-- iterate buong object within our notes array and render the html -->
          <!--  key para different id every object -->
          <p class="main-text"> {{note.text}}</p>
          <p class="date"> {{note.date}}</p>

          <button class="delete-btn" @click="deleteNote(note.id)">Delete</button>
        </div>
      </div>
    </div>
  </main>  
</template>

<script setup>
import { ref } from 'vue'

const showModal = ref(false)
const newNote = ref('')
const notes = ref([])
const deleteNote = (id) => {
  notes.value = notes.value.filter(note => note.id !== id)
}


const addNote = () => {
  notes.value.push({ // push para pumasok sa array natin na note
    text: newNote.value, // tesxt area 
    date: new Date().toLocaleString(), 
    //  yung local string para lang sa time na meron tau
    id: Math.floor(Math.random() * 10000),
    backgroundColor: `#${Math.floor(Math.random() * 16777215).toString(16)}`
  })

  // other way for bg color para dynamic sa java script

// function getRandomColor() {
//   var letters = '0123456789ABCDEF';
//   var color = '#';
//   for (var i = 0; i < 6; i++) {
//     color += letters[Math.floor(Math.random() * 16)];
//   }
//   return color;
// }

// function setRandomColor() {
//   $("#colorpad").css("background-color", getRandomColor());
// }


// OR

// function getRandomColor() {
//   color = "hsl(" + Math.random() * 360 + ", 100%, 75%)";
//   return color;
// }

  // reset states AFTER pushing
  newNote.value = ''
  showModal.value = false
}
</script> 


<style>
main{
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
  border-radius: 100px;
  color: white;
  background-color: rgb(21,20,20);
  font-size: 20px;
}

.card {
  width: 225px;
  height: 225px;
  padding: 10px;
  background-color: rgb(203, 113, 113);
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 20px;
  margin-bottom: 20px;
}

.date{
  font-size: 12.5px;
  font-weight: bold;
}

.cards-container{
  display: flex;
  flex-wrap: wrap;
}

.overlay{
  position: absolute;
  height: 100%;
  width: 100%;
  background-color: rgba(0, 0, 0, 0.7);
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal {
  width: 750px;
  background-color: white;
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
  background-color: rgb(21,20,20);
  border: none;
  color: white;
  cursor: pointer;
  margin-top: 15px;
}

.close {
  background: red;
  position: absolute;
  top: 10px;
  right: 10px;
  width: 20px;
  height: 20px;
  cursor: pointer;
}

.delete-btn{
  border: none;
  padding: 6px 10px;
  border-radius: 8px;
  cursor: pointer;
  background: rgba(0,0,0,0.25);
  color: #fff;
  font-weight: bold;
  align-self: flex-end;
}


</style>
