<script setup>

const props = defineProps({
  data: Object,
  sortItems:Function,
})
import tableColumn from './tableColumn.vue';
import modals from './modals.vue';
import icons from './svgIcons.vue'
import pagination from './pagination.vue'

</script>
<template>
  <main>
    <div class="container">
      <table class="table table-hover">
        <thead>
          <tr >
            <th  class="cursor-pointer" scope="col" @click = "sortItems" data-sort="name">Название</th>
            <th  class="cursor-pointer" scope="col" @click = "sortItems" data-sort="owner">ФИО директора <icons class="bi-arrow-down" color="#000" /> </th>
            <th  scope="col">Номер телефона</th>
            <th  scope="col"></th>
          </tr>
        </thead>
        <tbody>
          <tableColumn v-for = "(item) in props.data" 
            :item = item
          />
        </tbody>
      </table>
      <pagination />
    </div>
    <modals 
    :toggle="toggleModal" 
    :checkInputs="checkInputs" 
    />
  </main>
</template>

<style>

</style>
