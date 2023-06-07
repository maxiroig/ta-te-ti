<script setup>
import {ref, watch} from 'vue';
import cross from '/public/images/close.png'
import circle from '/public/images/circle.png'
import Modal from '@/components/Modal.vue'
const cells = [
    [
        {
            id: 1,
            movement: null,
            filled: false,
            class: null,
        },
        {
            id: 2,
            movement: null,
            filled: false,
            class: null,
        },
        {
            id: 3,
            movement: null,
            filled: false,
            class: null,
        }
    ],
    [
        {
            id: 4,
            movement: null,
            filled: false,
            class: null,
        },
        {
            id: 5,
            movement: null,
            filled: false,
            class: null,
        },
        {
            id: 6,
            movement: null,
            filled: false,
            class: null,
        }
    ],
    [
        {
            id: 7,
            movement: null,
            filled: false,
            class: null,
        },
        {
            id: 8,
            movement: null,
            filled: false,
            class: null,
        },
        {
            id: 9,
            movement: null,
            filled: false,
            class: null,
        }
    ]
]; 
const winningCells = [
    [1,2,3],
    [4,5,6],
    [7,8,9],
    [1,5,9],
    [2,5,8],
    [3,5,7],
    [1,4,7],
    [3,6,9],
];
const props = defineProps({playerTurn: String})

const player1cells= ref([]);
const player2cells= ref([]);
let modalActive = ref(false);
let validationApproved = ref(false);
const playerActive = ref(props.playerTurn)

function cellClicked(id){
    validationApproved = false;
    validations(id);
    if(playerActive.value === "Player 1" && validationApproved){
        assignCross(id)
    }
    if(playerActive.value === "Player 2" && validationApproved){
        assignCircle(id)
    }
    
};

const assignCross = (id) => {
    cells.value = cells.map((cell) => {
        cell.map((c)=>{
            if(c.id === id && !c.filled){
                c.movement = cross;
                c.filled = true;
                c.class = "cross"
                player1cells.value.push(id)
            }
        })
    })
    checkWinner();
};

const assignCircle = (id) => {
    cells.value = cells.map((cell) => {
        cell.map((c)=>{
            if(c.id === id && !c.filled){
                c.movement = circle;
                c.filled = true;
                c.class = "circle"
                player2cells.value.push(id)
            }
        })
    })
    checkWinner();
};

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
};

const closeModal = () => {
    modalActive.value = false;
};

const changeActiveTurn = () => {
    if(playerActive.value === "Player 1"){
        playerActive.value = "Player 2"
    }else {
        playerActive.value = "Player 1"
    }
};

const checkWinner = () => {
    let cellId = null;
    console.log("player1", player1cells.value);
    
    cells.map((cell) => {
        cell.map((c)=> {
            console.log("c", c.is(item => item.class === "cross"));
            //cellId = c.is(c.class, 'cross')
        })
    })
    console.log("cell", cellId);
    /* let winningMovements = null;

    winningCells.map((cell) => {
        winningMovements = JSON.stringify(cell.sort(function(a, b){return a - b}));
    })
    if (winningMovements.includes(playerMovements)){
        console.log("winner");
    }
    console.log("winning", winningMovements); */
};

watch(player1cells.value, (newValue) => {
    let firstFilter = null;
    let secondFilter = null;
    let thirdFilter = null;
    
    
});
watch(player2cells.value, (newValue) => {
    console.log("player2", player2cells.value);
});
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