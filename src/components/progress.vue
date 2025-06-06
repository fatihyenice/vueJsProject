<template>
    <h3>
        {{ actuel + 1 }} sur {{ max + 1 }}
    </h3> 

    <progress :value="actuel" :max="max"></progress>
</template>

<script setup>
defineProps({
    actuel: Number,
    max: Number
})
</script>