<template>
    <div>
        <button :class="class" @click="emit('cambiar')"> {{ title }}</button>
    </div>
</template>

<script setup>

let props = defineProps({
    title: String,
    class: String,
})

let emit = defineEmits(['cambiar'])
</script>