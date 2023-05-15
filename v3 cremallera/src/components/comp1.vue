<template>
    <div>
        <h4>hola {{ nombre }} esta es mi ganancia con interes {{ calculo }}</h4>
    </div>
</template>

<script setup>

defineProps({

    nombre: String,
    calculo: Number,

})
</script>