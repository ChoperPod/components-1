<script setup>
//defineProps(['title', 'id', 'body', "colorText"])
defineProps({
    title: String,
    id: Number,
    colorText: String,
    body: {
        type: String,
        default: 'Sin descripcion'
    },
    CambiarFavorito: Function
});
const emit = defineEmits(["CambiarFavorito"]);
</script>

<template>
    <div class="card">
        <h1>APP</h1>
        <div class="card-body">
            <h5 class="card-tittle">{{ id }} - {{ title }}</h5>
            <p>{{ body }}</p>
            <button @click="CambiarFavorito(title)" class="btn btn-outline-primary">Favorito</button>
        </div>
    </div>
</template>