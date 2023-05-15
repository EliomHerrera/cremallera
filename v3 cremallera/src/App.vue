<template>
    <div class="border p-5">
        <div class="header d-flex justify-content-between w-100">
            <img src="https://www.fprdireccioneshidraulicas.com.ar/post/cremallera-hidraulica-big.jpg" width="300"
                height="150">
            <h1 style="font-size: 4rem;"><span class="text-primary">Eliom</span> <span
                    class="badge bg-secondary">Cremalleras</span></h1>
            <h5 class="menu">
                <RouterLink active-class="text-primary" class="me-3" to="home">Home</RouterLink>
                <RouterLink active-class="text-primary" class="me-3" to="cremallera">Cremallera</RouterLink>
            </h5>
        </div>
        <RouterView />
    </div>
</template>