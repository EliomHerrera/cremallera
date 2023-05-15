<template>
    <div>
        <h1>Lista de cremalleras</h1>
        <ul v-for="elemento, index in cremallera" :key="elemento">
            <li>{{ index + 1 }} : {{ elemento.model }}</li>
        </ul>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    components: {
    },
    data: () => ({
        cremallera: []
    }),
    methods: {
        ver() {
            axios.get('http://localhost:3000/cremallera').then(res => {
                this.cremallera = res.data
            })
        }
    },
    mounted() {
        this.ver()
    },

}
</script>