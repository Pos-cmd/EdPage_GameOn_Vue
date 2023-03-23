<script setup>
import { ref } from 'vue';
import Main from './Main.vue';
import Form from './Form.vue';

const isFormShow = ref(false);


function toggleForm() {
  isFormShow.value = !isFormShow.value;
}

</script>

<template>
  <Main :class="{ displayFlex: !isFormShow, displayNone: isFormShow }" @show-form="toggleForm" />
  <Form :class="{ displayBlock: isFormShow, displayNone: !isFormShow }" @close-form="toggleForm" />
</template>