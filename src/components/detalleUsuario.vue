<template>
    <div>
        <div class="container">
            <img class="foto" :src="foto" alt="Foto de usuario" v-if="foto" />
            <p>{{ nombre }}</p>
            <p>{{ email }}</p>
        </div>
    </div>

</template>

<script>
export default {
    name: 'detalleUsuario',
    props: ["nombre", "email", "foto"],
}
</script>

<style scoped>  

.container {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.foto {
    width: 500px;
    height: 500px;
}
</style>