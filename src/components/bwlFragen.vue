<template>
    <div class="container">
        <div class="inhalt">
            <label for="">Stichworte: (Mit einem Komma trennen)</label>
            <input v-model="form.stichpunkte" type="text">
            <button @click="sendData()">Senden</button>
            <textarea name="textarea" id="textarea" cols="30" rows="10" readonly></textarea>
        </div>
    </div>
</template>

<script setup>
import axios from 'axios'
import { reactive } from 'vue'

const form = reactive({
    stichpunkte: ''
})

function sendData() {
    axios
    .get("http://localhost:8080/getBWLFragen", {
        params: {
            stichpunkte: form.stichpunkte
        },
    })
    .then(function (response){
        document.getElementById('textarea').value = response.data;
    })
    .catch(function (error){
        console.log(error);
    });
}
</script>

<style scoped>
.container{
    display: flex;
    justify-content: center;
}
.inhalt{
    display: flex;
    flex-direction: column;
    align-items: center;
}

input{
    width: 400px;
    height: 30px;
    margin-top: 5px;
    margin-bottom: 10px;
}

textarea{
    width: 800px;
    height: 200px;
    margin-top: 10px;
    margin-bottom: 10px;
    outline: none;
    resize: none;
    overflow: auto;
    
}

label{
    font-size: 1.2em;
}
</style>
