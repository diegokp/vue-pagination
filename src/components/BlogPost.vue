<script setup>

// defineProps(['title', 'id', 'body', 'colorText'])

defineProps({
    title: String,
    id: Number,
    body: {
        type: String,
        default: 'Sin descripción'
    }
});

const emit = defineEmits(['cambiarFavName'])

</script>


<template>
    <div class="card mb-2">
        <div class="card-body">
            <h5 class="card-title"
            
            >{{ id }} - {{ title }}</h5>
            <p>{{ body }}</p>
            <button @click="emit('cambiarFavName', title)" class="btn btn-outline-primary">Favorito</button>
        </div>
    </div>
</template>