<script setup>
import {ref} from 'vue';
import cross from '/public/images/close.png'
import circle from '/public/images/circle.png'
import Modal from '@/components/Modal.vue'
const cells = [
    [
        {
            id: 1,
            movement: null,
            filled: false,
        },
        {
            id: 2,
            movement: null,
            filled: false,
        },
        {
            id: 3,
            movement: null,
            filled: false,
        }
    ],
    [
        {
            id: 4,
            movement: null,
            filled: false,
        },
        {
            id: 5,
            movement: null,
            filled: false,
        },
        {
            id: 6,
            movement: null,
            filled: false,
        }
    ],
    [
        {
            id: 7,
            movement: null,
            filled: false,
        },
        {
            id: 8,
            movement: null,
            filled: false,
        },
        {
            id: 9,
            movement: null,
            filled: false,
        }
    ]
]; 

let validationApproved = ref(false);
const props = defineProps({playerTurn: String})
const playerActive = ref(props.playerTurn)
let modalActive = ref(false);

function cellClicked(id){
    validationApproved = false;
    validations(id);
    if(playerActive.value === "Player 1" && validationApproved){
        assignCross(id)
    }
    if(playerActive.value === "Player 2" && validationApproved){
        assignCircle(id)
    }
}
const assignCross = (id) => {
    cells.value = cells.map((cell) => {
        cell.map((c)=>{
            if(c.id === id && !c.filled){
                c.movement = cross;
                c.filled = true;
            }
        })
    })
}
const assignCircle = (id) => {
    cells.value = cells.map((cell) => {
        cell.map((c)=>{
            if(c.id === id && !c.filled){
                c.movement = circle;
                c.filled = true;
            }
        })
    })
}
const validations = (id) => {
    cells.value = cells.map((cell) => {
        cell.map((c)=>{
            if(c.id === id && c.filled === true){
                modalActive.value = true;
                validationApproved = false;
            }else{
                validationApproved = true;
                changeActiveTurn();
            }
        })
    })
}
const closeModal = () => {
    modalActive.value = false;
}
const changeActiveTurn = () => {
    if(playerActive.value === "Player 1"){
        playerActive.value = "Player 2"
    }else {
        playerActive.value = "Player 1"
    }
};
/* watch(playerActive, (newValue) => {
    console.log("player", newValue);
}) */
</script>
<template>
    <div class="text-center text-white text-2xl">
        Turn Active: {{ playerActive }} 
    </div>
    <Modal 
    :isOpen="modalActive"
    @closeModal="closeModal"/>
    <div class="bg-white w-full h-full rounded-3xl">

        <div id="grid-table"
        v-for="(column, index) in cells" :key="index"
        class="grid grid-cols-3 h-1/3">
            <div
            v-for="(cell, index) in column" :key="index"
            @click="cellClicked(cell.id)"
            class="border-2 border-black  text-white flex justify-center items-center "> 
                <img :src="cell.movement" alt="" style="width: 150px;">
            </div>
        </div>
    </div>
    <div v-if="!validationApproved">
        {{ errorMessage }}
    </div>
    <div >
        
    </div>
</template>

<style scoped>

</style>