<script setup>
import {inject} from "vue"
import icons from './svgIcons.vue'

const props = defineProps({
    pageChange:Function,
    page:Number,
    allItems:Number,
})

const page =  inject('page');
const allItems = inject('allItems');
const pageChange = inject('pageChange');

</script>
<template>
    <div class="pagination pagination-lg">
        <button class="btn btn-primary btn-sm" :disabled="page === 1" data-page = "prev" @click = pageChange ><icons class="bi-arrow-left" color="#fff" /></button>
            <div class="page-num">Страница {{ page }} </div>
        <button class="btn btn-primary btn-sm" :disabled="page === Math.ceil(allItems/4)" data-page = "next" :data-limit = "Math.ceil(allItems/4)" @click = pageChange ><icons class="bi-arrow-right" color="#fff" /></button>
    </div>
</template>
<style>
.pagination{
    align-items: center;
    justify-content: flex-end;
}

.page-num{
    margin: 0 20px;
}

.btn svg{
    pointer-events: none;

}
</style>