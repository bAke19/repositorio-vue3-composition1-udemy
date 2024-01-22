<script setup>
//defineProps(['title', 'text', 'colorText'])
defineProps({
    title:String,
    id: Number,
    text:{
        type: String,
        default: 'Sin descripcion'
    },
    colorText: String,
    //cambiarFavoritoNombre:Function
})

const emit = defineEmits(['cambiarFavoritoNombre'])

//emit('cambiarFavoritoNombre', title)
</script>

<template>
    <div class="card">
        <div class="card-body">
            <h5 class="card-title">
               {{ id }} - {{title}}
            </h5>
            <p>
                {{ text }}
            </p>
            <button
                class="btn btn-sm btn-outline-primary"
                @click="emit('cambiarFavoritoNombre', title)"
            >
                Mi Favorito
            </button>
        </div>
    </div>
</template>