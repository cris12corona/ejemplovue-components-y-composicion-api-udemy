<script setup>
defineProps(["inicio", "final","maxLength"]);

const emit = defineEmits(['next','previus'])
const activarSiguiente = () => {
    console.log('me diste sigiuiente')
    emit("next")
};
</script>
<template>
    <div class="btn-group" role="group" aria-label="Basic example">
  <button type="button" class="btn btn-outline-primary" 
  @click="$emit('previus')" :disabled="inicio === 0">Previus {{ inicio }}</button>
  <button type="button" class="btn btn-outline-primary"
   @click="activarSiguiente"
   :disabled="final >= maxLength"
   >Next {{ final }}</button>
</div>
</template>