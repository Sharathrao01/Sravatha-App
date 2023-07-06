<script setup>
import {ref} from "vue";
const showModel = ref(false);
const newNote = ref("");
const notes = ref([]);

function getRandomColor() {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
  
}
const addNote = () => {
  if(newNote.value.length<=9)
  {
    alert("New note must contain more than 10 charecters!");
    return;
  }
  notes.value.push({
    id: Math.floor(Math.random() * 1000000),
    text: newNote.value,
    date : new Date(),
    backgroundColor : getRandomColor()
  })
  showModel.value = false
  newNote.value = ""
}

</script>

<template>
  <main>
    <div v-if="showModel" class="overlay">
      <div class="model">
        <textarea v-model.trim="newNote" name="note" id="note" cols="30" rows="10"></textarea>
        <button @click="addNote">Add Note</button>
        <button class="close" @click="showModel = false">Close</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes </h1>
        <button @click="showModel = true">Add</button>
      </header>
      <div class="cards-container">
        <div v-for="note in notes" 
        :key = "note.id"
        class="card" 
        :style="{backgroundColor:note.backgroundColor}">  
          <p class="main-text">{{ note.text }}</p>
          <p class="date">{{ note.date }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
main{
  height: 100vh;
  width: 100vw;
}
.container{
max-width: 1000px;
padding: 10px;
margin: 0 auto;
}

header{
  display: flex;
  justify-content: space-between;
  align-items: center;
}

h1{
 font-family: 'Times New Roman', Times, serif;
 font-size: 80px;
}
header button{
  background-color: rgb(221, 224, 13);
  height: 40px;
  width: 60px;
  font-size: larger;
  border-radius: 20%;
  padding: 10px;
}
button{
  background-color: rgb(247, 231, 3);
  font-family: 'Times New Roman', Times, serif;
  font-size: larger;
  cursor: pointer;
  padding: 10px 20px;
  margin-top: 10px;

}
#notes{
  font-family: 'Times New Roman', Times, serif;
  font-size: large;
  font-weight: bold;
}
header button:hover {
  background-color: rgb(245, 115, 10);
  cursor: pointer;
}
.card{
  width: 225px;
  height: 225px;
  background-color: rgb(9, 245, 186);
  border-radius: 15px;
  display: flex;
  padding: 10px;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 20px;
  margin-bottom: 20px;
}
.cards-container{
  display: flex;
  flex-wrap: wrap;
}
.overlay{
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(0,0,0,0.77);
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;
}
.model{
  width: 750px;
  background-color: antiquewhite;
  border-radius: 10px;
  padding: 30px;
  position: relative;
  display: flex;
  flex-direction: column;
}
.close{
  background-color: rgb(226, 16, 16);
  font-family: 'Times New Roman', Times, serif;
  font-size: larger;
  cursor: pointer;
  padding: 10px 20px;
  margin-top: 10px;
}
</style>