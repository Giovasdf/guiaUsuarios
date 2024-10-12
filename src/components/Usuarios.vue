<template>
    <div>
        <img :src="foto" alt="Foto de usuario" v-if="foto" /> 
        <br>
        <button @click="$emit('eliminar', email)">Eliminar</button>
    </div>
</template>

<script>
export default {
    name: 'Usuarios',
    props: ["foto", "email", "nombre"],
}
</script>

<style scoped>
img {
    width: 100px;
    height: 100px; 
}
</style>
