<script setup>

import {inject} from "vue"

const props = defineProps({
    item:Object,
    deleteItem:Function
})

const deleteItem = inject("deleteItem")

function buildPhone(){
    let phoneNums = props.item.phone.split("");
    let phone = [];
    if(phoneNums.length === 12){
        for(let i = 0; i < phoneNums.length; i++){
            if(i != 1 && i != 4 && i != 7 && i != 9){
                phone.push(phoneNums[i]);
            } else {
                phone.push(phoneNums[i] + " ");  
            }
        }
    } else if(phoneNums.length === 11){
        for(let i = 0; i < phoneNums.length; i++){
            if(i != 0 && i != 3 && i != 6 && i != 8){
                phone.push(phoneNums[i]);
            } else {
                phone.push(phoneNums[i] + " ");  
            }
        }
    }else{
        for(let i = 0; i < phoneNums.length; i++){
                phone.push(phoneNums[i]);
        }
    }   
    return phone.join("")
} 

</script>
   
<template>
    <tr>
        <th scope="row"> {{props.item.name}} </th>
        <td> {{props.item.owner}} </td>
        <td> {{buildPhone()}} </td>
        <td class="close_btn" align="center">
            <button @click = deleteItem type="button" class="btn-close" :data-item = props.item.id></button>
        </td>
    </tr>
</template>

<style scoped></style>