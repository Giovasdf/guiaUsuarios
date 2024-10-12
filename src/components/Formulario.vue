<template>
    <div>
        <form @submit.prevent="agregarUsuario">
            <div class="container">
                <div>
                    <label for="nombre">Nombre:</label>
                    <input type="text" name="nombre" id="nombre" v-model="nombre" required />
                </div>
                <div>
                    <label for="foto">Foto:</label>
                    <input type="text" name="foto" id="foto" v-model="foto" required />
                </div>
                <div>
                    <label for="email">Email:</label>
                    <input type="email" name="email" id="email" v-model="email" required />
                </div>
                <div>
                    <button type="submit">Agregar</button>
                    <input type="reset" value="Limpiar" @click="limpiarCampos" />
                </div>
            </div>
        </form>

        <div>
            <ul>
                <li v-for="usuario in usuarios" :key="usuario.email">
                    <Usuarios 
                        :nombre="usuario.nombre" 
                        :email="usuario.email" 
                        :foto="usuario.foto" 
                        @eliminar="eliminarUsuario(usuario.email)" />
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
import Usuarios from './Usuarios.vue'; 

export default {
    name: 'Formulario',
    components: {
        Usuarios 
    },
    data() {
        return {
            usuarios: [],
            nombre: '',
            email: '',
            foto: ''
        };
    },
    methods: {
        agregarUsuario() {
            if (this.usuarios.find(usuario => usuario.email === this.email)) {
                alert('Este email ya está registrado.');
                return;
            }
            this.usuarios.push({ nombre: this.nombre, email: this.email, foto: this.foto });
            this.limpiarCampos();
        },
        limpiarCampos() {
            this.nombre = '';
            this.email = '';
            this.foto = '';
        },
        eliminarUsuario(email) {
            this.usuarios = this.usuarios.filter(usuario => usuario.email !== email);
        }
    }
}
</script>

<style scoped>
form {
    background-color: black;
    color: white;
    width: 200px;
    padding: 20px;
}

.container {
    flex-direction: column;
    align-items: left;
    display: block;
}
</style>
