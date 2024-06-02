<script setup>
import {inject} from "vue"

const props = defineProps({
  visible:Boolean,
  checkInputs:Function,
  modalDisabled:Boolean
})

const modalDisabled = inject('modalDisabled');
const show_modal = inject('show_modal');
const addNew = inject('addNew');
const toggleModal = inject('toggleModal');
const checkInputs = inject('checkInputs');

</script>
<template>
  <div v-if="show_modal == true" class="modal show">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h4 class="modal-title" id="staticBackdropLiveLabel">Добавить организацию</h4>
          <button @click = toggleModal type="button" class="btn-close"></button>
        </div>
        <form @submit = "addNew" >
          <div class="modal-body">
            <input type="text" @change=checkInputs  name="org" class="form-control" required placeholder="Название" />
            <input type="text" @change=checkInputs  name="phoneNum" class="form-control" required placeholder="Номер телефона" />
            <input type="text" @change=checkInputs  name="own" class="form-control" required placeholder="ФИО директора" />
          </div>
          <div class="modal-footer">
            <button @click = toggleModal type="button" class="btn btn-secondary">Отмена</button>
            <button :disabled="modalDisabled === true"  type="submit" class="btn btn-primary">Ок</button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<style scoped>
.modal {
  display: none;
  position: fixed;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  background-color: rgba(0, 0, 0, 0.3);
}

.modal.show {
  display: block;
}

.modal-body .form-control:not(:last-child) {
  margin-bottom: 15px;
}
</style>
