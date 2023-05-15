
<script>
export default {
    data: () => ({
        ocultar: 0, url: '', model: '', year: '', price: '', available: '', cremallera: [], mensaje: 0
    }),
    methods: {
        ver() {

            this.cremallera = []

            axios.get('http://localhost:3000/cremallera')

                // .then(res => {
                //     for (let i of res.data) {
                //         this.cremallera.push(i)
                //     }
                // })

                .then(res => {
                    this.cremallera = res.data
                })

        },
        vaciar() {
            this.url = ""
            this.model = ""
            this.year = ""
            this.price = ""
            this.available = ""
        },
        fnClose() {
            this.vaciar()
            this.ver()
            this.ocultar = 0
            this.mensaje = 0
        },
        fnSave() {
            if (this.url == '' || this.model == '' || this.year == '' || this.price == '' || this.available == '') {
                this.mensaje = 1
                return
            }

            axios.post('http://localhost:3000/cremallera', {
                url: this.url, model: this.model, year: this.year, price: this.price, available: this.available,
            })

            this.vaciar()
            this.ver()

            this.ocultar = 1
            this.mensaje = 0
        },
        fnDel(index) {
            let id = this.cremallera[index].id
            axios.delete('http://localhost:3000/cremallera/' + id)
            this.ver()

        },
    },
    mounted() {
        this.ver()
    },
}
</script>
<template>
    <div class="border my-4 p-5">
        <div class="d-flex justify-content-around">
            <RouterLink class="m-3" to="listaCremallera">Listas de Cremalleras</RouterLink>

            <h5>Agregar Cremallera
                <!-- Button trigger modal -->
                <button type="button" class="btn btn-primary mx-3" data-bs-toggle="modal"
                    data-bs-target="#exampleModal">+</button>
                <!-- Modal -->
                <div class="modal fade " id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel"
                    aria-hidden="true">

                    <div class="modal-dialog">

                        <div class="modal-content">

                            <div class="modal-header">
                                <h5 class="modal-title text-dark mx-5" id="exampleModalLabel">
                                    Caracteristicas De La Cremallera
                                </h5>
                                <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                            </div>

                            <div class="modal-body text-dark">
                                <div>
                                    <img :src="url" width="200">
                                </div>
                                <div v-show="ocultar == 1" class="alert alert-primary text-center" role="alert">
                                    Ha sido guardado
                                </div>
                                <div v-show="mensaje == 1" class="alert alert-danger text-center" role="alert">
                                    Hay campos *** Vacios ***
                                </div>
                                <div class="row w-50">
                                    <p>url <input v-model="url" type="text"></p>
                                    <p>model <input v-model="model" type="text"></p>
                                    <p>year <input v-model="year" type="number"></p>
                                    <p>price <input v-model="price" type="number"></p>
                                    <p>Quantity Available <input v-model="available" type="number"></p>
                                </div>
                            </div>
                            <div class="modal-footer">
                                <button type="button" class="btn btn-secondary" @click="fnClose()"
                                    data-bs-dismiss="modal">Close</button>
                                <button type="button" class="btn btn-primary" @click="fnSave()">Save</button>
                            </div>
                        </div>
                    </div>
                </div>
            </h5>
        </div>
        <hr>
        <div class="m-4 p-4">
            <h1 class="text-center text-white bg-primary my-5 p-4">Cremalleras</h1>
            <div class="border d-flex flex-wrap justify-content-start">


                <div class="m-2 " v-for="crema, index in cremallera">

                    <div class="card p-2 m-1" style="width: 12rem;">
                        <img :src=crema.url width="100" height="100" class="card-img-top">
                        <div class="card-body text-dark text-center">
                            <h6 class="text-info">Modelo: {{ crema.model }}</h6>
                            <hr>
                            <h6 class="text-warning">Año: {{ crema.year }}</h6>
                            <hr>
                            <h6 class="text-success">Precio: {{ crema.price }}</h6>
                            <hr>
                            <h6 class="text-danger">Disponible: {{ crema.available }}</h6>
                            <hr>

                            <div>
                                <button class="btn btn-danger me-2" @click="fnDel(index)">X</button>
                            </div>

                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>