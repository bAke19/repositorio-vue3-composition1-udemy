<script setup>

import {ref} from  "vue";
const props = defineProps(["inicio", "final", "max"])

const deseablePrev = ref(false)
const deseableNext = ref(false)

const emit = defineEmits(['nextPage', 'previewPage'])

</script>

<template>
    <div class="btn-group" role="group" aria-label="Basic example">
        <button type="button" class="btn btn-outline-primary" @click="emit('previewPage')" :disabled="inicio === 0">Preview {{ inicio }}</button>
        <button type="button" class="btn btn-outline-primary" @click="emit('nextPage')" :disabled="final  >= max ">Next {{ final }}</button>
    </div>
</template>