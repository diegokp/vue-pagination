<script setup>
defineProps(["inicio", "fin", "maxLength"]);
const emit = defineEmits(['prev', 'next'])

</script>

<template>
    <div class="btn-group mb-2" role="group" aria-label="Basic example">
        <button 
            type="button" 
            class="btn btn-primary" 
            @click="emit('prev')" 
            :disabled="inicio <= 0"
        >
            Preview {{ inicio }}
        </button>
        <button t
            ype="button" 
            class="btn btn-primary" 
            @click="emit('next')"
            :disabled="fin >= maxLength"
        >
            Next {{ fin }}
        </button>
    </div>
</template>