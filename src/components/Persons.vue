<script setup lang='ts'>
import { ref, Ref } from 'vue'
import PersonsPostForm from './PersonsPostForm.vue';
import PersonsList from './PersonsList.vue';
import PersonData from '../Persons.json'

export type Person = {
    id: number,
    name: string
    age: number
}
const persons: Ref<Person[]> = ref(PersonData);
const registerPerson = (person: Person) => {
    persons.value.push(person);
}
const deletePerson = (id: number) => {
    persons.value = persons.value.filter(person => person.id !== id);
}
 
</script>

<template>
<div class="container"> 
    <h1>Title</h1>
    <PersonsPostForm @register="registerPerson"/> 
    <div class="List-container">
        <ul>
            <PersonsList :persons="persons" @delete="deletePerson" />
        </ul>
    </div>
</div>
</template>

<style scoped>
.container {
    display: flex;
    flex-direction: column;
    align-items: center;
}
</style>