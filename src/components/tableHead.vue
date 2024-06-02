<script setup>

const props = defineProps({
  toggleModal:Function,
  itemsFilter:Function,
})

</script>
<template>
  <header>
    <div class="container header_container">
      <input @input = itemsFilter type="text" class="form-control" placeholder="Найти по ФИО..." />
      <button
        @click = toggleModal
        type="button"
        class="btn btn-primary"
      >
        Добавить
      </button>
    </div>
  </header>
</template>

<style scoped>
header {
  padding-top: 7%;
}
.header_container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 30px;
}
.form-control {
  max-width: 300px;
}
</style>
