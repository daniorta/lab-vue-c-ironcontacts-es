<script setup>
import { ref } from 'vue';
import contactsData from "./contacts.json";

const contacts = ref((contactsData.slice(0, 5)));

const addRandomContact = () => {
    const randomIndex = Math.floor(Math.random() * contactsData.length);
    const randomContact = contactsData[randomIndex];

    const exists = contacts.value.find(contact => contact.id === randomContact.id)
    if (!exists) {
        contacts.value.push(randomContact);
    }
}

const popularitySort = () => {
     contacts.value.sort((a, b) =>   b.popularity - a.popularity )

}


const nameSort = () => {
    contacts.value.sort((a, b) => a.name.localeCompare(b.name))
}

const deleteContact = (id) => {
    const index = contacts.value.findIndex(contact => contact.id === id) 
    if (index !== -1) {
        contacts.value.splice(index, 1)
    }
}

</script>

<template>
    <section class="container-table">

        <h1 class="title">IronContacs</h1>

        <div class="container-button">
            <button @click="addRandomContact" class="button-nav">Add Random Contct</button>
            <button @click="popularitySort" class="button-nav">Sort by popularity</button>
            <button @click="nameSort" class="button-nav">Sort by name</button>

        </div>

        <table>
            <thead>
                <tr>
                    <th class="index">Picture</th>
                    <th class="index">Name</th>
                    <th class="index">Popularity</th>
                    <th class="index">Won Oscar</th>
                    <th class="index">Won Emmy</th>
                    <th class="index">Actions</th>
                </tr>
            </thead>

            <tbody>
                <tr v-for="contact in contacts" :key="contact.id">
                    <td><img class="image" :src="contact.pictureUrl" alt="Picture od {{ contact.name }}"></td>
                    <td class="name">{{ contact.name }}</td>
                    <td class="popularity">{{ contact.popularity.toFixed(2) }}</td>
                    <td>
                        <i v-if="contact.wonOscar">🏆</i>
                    </td>
                    <td>
                        <i v-if="contact.wonEmmy">⭐️</i>
                    </td>
                    <td>
                        <button @click="deleteContact(contact.id)" class="delete">Delete</button>
                    </td>
                </tr>
            </tbody>

        </table>
    </section>


</template>

<style>
body {
    font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
}

.container-table {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;

}

.title {
    font-size: 4em;
}

.container-button {
    display: flex;
    gap: 20px;

    .button-nav {
        height: 30px;
        margin-bottom: 40px;
        font-size: 1.2em;
    }
}


.index {
font-size: 1.2em;
padding: 10px;}


.image {
    width: 100px;
    margin: 20px;
}

.name, .popularity{
    padding: 10px;
    font-size: 1.5em;
}

.delete{
    width: 70px;
    height: 30px;
}


   

</style>
