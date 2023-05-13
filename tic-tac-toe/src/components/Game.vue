<script setup>
import { reactive, ref, watch } from 'vue';
const cells = [
    [
        {
            id: 1,
            class: "",
            filled: false
        },
        {
            id: 2,
            class: "",
            filled: false
        },
        {
            id: 3,
            class: "",
            filled: false
        }
    ],
    [
        {
            id: 4,
            class: "",
            filled: false
        },
        {
            id: 5,
            class: "",
            filled: false
        },
        {
            id: 6,
            class: "",
            filled: false
        }
    ],
    [
        {
            id: 7,
            class: "",
            filled: false
        },
        {
            id: 8,
            class: "",
            filled: false
        },
        {
            id: 9,
            class: "",
            filled: false
        }
    ]
]; 

const props = defineProps({playerTurn: String})

const playerActive = ref(props.playerTurn)

function cellClicked(id){
    playerActive.value === "player 1" ? playerActive.value = "player 2" : playerActive.value = "player 1"

    console.log("playerActive", playerActive.value);
}
/* watch(playerActive, (newValue) => {
    console.log("player", newValue);
}) */
</script>
<template>
    <div class="text-center text-white">Turn Active: 
        {{  playerActive }} 
    </div>
    <div class="bg-white w-full h-full rounded-3xl">
        <div id="grid-table"
        v-for="(column, index) in cells" :key="index"
        class="grid grid-cols-3 h-1/3">
            <div
            v-for="(cell, index) in column" :key="index"
            @click="cellClicked(cell.id)"
            class="border-2 border-black  text-white flex justify-center items-center "> 
                <div 
                :class="cell.class"
                class="text-black text-center ">
                    {{ cell.name }}
                </div>
            </div>
        </div>
    </div>
</template>

<style>

</style>