<script setup>
import {ref} from "vue"
import { onMounted } from "vue";
import { provide } from "vue";
import axios from "axios";
import tableHead from "./components/tableHead.vue"
import tableBody from "./components/tableBody.vue"

let clients = ref();
let show_modal = ref(false);
let modalDisabled  = ref(true);
let page = ref(1);
let allItems = ref();
let sort = "";
let filter="";
let pageNum = 1;
const modalValues = {"phoneNum":"","own":"", "org":""};

provide("page" , page);
provide("modalDisabled" , modalDisabled);
provide("show_modal" , show_modal);
provide("allItems" , allItems);
provide("addNew" , addNew);
provide("deleteItem" , deleteItem);
provide("pageChange" , pageChange);
provide("toggleModal" , toggleModal);
provide("checkInputs" , checkInputs);

onMounted( async()=>{
  try{
    const {data} = await axios.get("https://4430e6b349c7b094.mokky.dev/clients?page=1&limit=4");
    clients.value = data.items;
    allItems.value = data.meta.total_items;
  } catch(error){
    console.log(error);
  }
})


function keyGenerate(){
  return 1 + Math.floor(Math.random() * (10000000 + 1 - 1));
}

function addNew(e){
  e.preventDefault();
  let newData= {"name":e.target.elements[0].value , 
  "phone":e.target.elements[1].value,
  "owner": e.target.elements[2].value,
  "id": keyGenerate(),
}
axios.post("https://4430e6b349c7b094.mokky.dev/clients" , newData).then(resp => update(sort, filter));
  toggleModal();

  
}

async function update(sort, filter , updatePage){
  let page = updatePage ? updatePage : 1;
  const {data} = await axios.get("https://4430e6b349c7b094.mokky.dev/clients?page="+page+"&limit=4"+sort+filter);
  clients.value = data.items;
  allItems.value = data.meta.total_items;
  return data
}

function deleteItem(e){
  let key = e.target.getAttribute('data-item');
  try{
    axios.delete("https://4430e6b349c7b094.mokky.dev/clients/"+key).then(response => {
      update(sort, filter)
  });
  }catch(error){
    console.log(error)
  }
}

function toggleModal(){
  show_modal.value = !show_modal.value;
  modalDisabled.value = true;
  modalValues.phoneNum = "";
  modalValues.own = "";
  modalValues.org = "";
}

function checkInputs(e){
  let target = e.target;
  modalValues[target.name] = e.target.value;
  let elems= (Object.values(modalValues));
  let validate = elems.every(elem => elem != "".trim());
  modalDisabled.value = !validate;
}

function itemsFilter(e){
  let trigger = "&owner=*";
  let value = e.target.value;
  filter = trigger + value;
  update(sort , filter)
}

function sortItems(e){
  let trigger = "&sortBy=";
  let value = e.target.getAttribute('data-sort');
  sort = trigger + value;
  update(sort , filter);
}

function pageChange(e){
let taget = e.target.getAttribute('data-page');

if(taget == "next"){
  pageNum++;
  update(sort,filter,pageNum);
  page.value = pageNum
}else if(taget == "prev"){
  pageNum--;
  update(sort,filter,pageNum);
  page.value = pageNum
}
}

</script>

<template>
  <tableHead :toggleModal="toggleModal" :itemsFilter = "itemsFilter"/>
  <tableBody :data="clients" 
  :sortItems = "sortItems"
  />
</template>