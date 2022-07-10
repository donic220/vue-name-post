<script setup lang='ts'>
import { defineProps,ref } from 'vue'
import { Person } from './Persons.vue'

type Props = {
    persons: Person[]
}

const emit = defineEmits(['delete'])
const isDialogOpne = ref<boolean>(false)
const confirmMsg = ref<string>('')

const onClickDelete = (name: string) => {
    isDialogOpne.value = !isDialogOpne.value;
    // if (confirm('Delete ' + name + '?')) {
    //     emit('delete', id)
    // }
    confirmMsg.value = 'Delete ' + name + '?'
}

const onClickDeleteOk = (id: number) => {
    emit('delete', id);
    isDialogOpne.value = !isDialogOpne.value;
}

const onClickDeleteCancel = () => {
    isDialogOpne.value = !isDialogOpne.value;
}

defineProps<Props>()
</script>

<template>
    <li v-for="person in persons" :key="person.id" class="person-list">
        <span>{{ person.name }}</span>
        <span>age: {{ person.age }}</span>
            <button @click="onClickDelete(person.name)">
            <span>delete</span>
        </button>
        <teleport to="body">
            <dialog class="dialog" :open="isDialogOpne">
                <span>Dialog
                    <br>{{ confirmMsg }}
                </span>
                <div class="dialog-footer">
                    <button class="ok-button" @click="onClickDeleteOk(person.id)">OK</button>
                    <button class="ng-button" @click="onClickDeleteCancel">Cancel</button>
                </div>
                </dialog>
        </teleport>
    </li>
</template>

<style scoped>
.person-list {
    list-style: none;
    margin-bottom: 12px;
    border-radius: 4px;
    font-size: 20px;
    font-weight: bold;
    display: flex;
    justify-content: space-between;
    background-color: rgb(228, 200, 133);
    padding: 8px 20px;
    width: 300px;
}

.dialog {
    position:absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    height: 100px;
    width: 300px;
    margin: auto;
    background-color: aliceblue;
}

.dialog-footer {
  display: flex;
  margin-top: 30px;
  height: 30px;
  width: 300px;
  justify-content: center;
  align-items: center;
}
.ok-button {
    display: flex;
    margin-right: 50px;
}

</style>