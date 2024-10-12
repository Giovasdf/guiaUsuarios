<template>
    <div class="layout">
        <aside class="sidebar">
            <div class="formulario">
                <form @submit.prevent="agregarUsuario">
                    <div class="input-container">
                        <label for="nombre">Nombre:</label>
                        <input type="text" name="nombre" id="nombre" v-model="nombre" required />
                    </div>
                    <div class="input-container">
                        <label for="foto">Foto:</label>
                        <input type="text" name="foto" id="foto" v-model="foto" required />
                    </div>
                    <div class="input-container">
                        <label for="email">Email:</label>
                        <input type="email" name="email" id="email" v-model="email" required />
                    </div>
                    <div class="button-container">
                        <button type="submit">Agregar</button>
                        <input type="reset" value="Limpiar" @click="limpiarCampos" />
                    </div>
                </form>
            </div>

            <div class="lista-usuarios">
                <h3>Listado de Usuarios</h3>
                <ul>
                    <li v-for="usuario in usuarios" :key="usuario.email">
                        <Usuarios 
                            :nombre="usuario.nombre" 
                            :email="usuario.email" 
                            :foto="usuario.foto" 
                            @eliminar="eliminarUsuario(usuario.email)" 
                            @ver-detalle="mostrarDetalle(usuario)" />
                    </li>
                </ul>
            </div>
        </aside>

        <div class="detalle-usuario" v-if="usuarioSeleccionado">
            <detalle-usuario 
                :nombre="usuarioSeleccionado.nombre" 
                :email="usuarioSeleccionado.email" 
                :foto="usuarioSeleccionado.foto"
                @close="usuarioSeleccionado = null" /> 
        </div>
    </div>
</template>

<script>
import Usuarios from './Usuarios.vue'; 
import detalleUsuario from './detalleUsuario.vue'; 

export default {
    name: 'Formulario',
    components: {
        Usuarios,
        detalleUsuario 
    },
    data() {
        return {
            usuarios: [],
            nombre: '',
            email: '',
            foto: '',
            usuarioSeleccionado: null 
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
        },
        mostrarDetalle(usuario) {
            this.usuarioSeleccionado = usuario; 
        }
    }
}
</script>

<style scoped>
.layout {
    display: flex; 
    height: 100vh; 
}

.sidebar {
    width: 300px; 
    background-color: black; 
    color: white; 
    padding: 20px; 
    box-shadow: 2px 0 5px rgba(0, 0, 0, 0.5); 
}

.detalle-usuario {
    flex-grow: 1; 
    padding: 20px; 
    background-color: #f9f9f9; 
}

.formulario, .lista-usuarios {
    margin-bottom: 20px; 
}

.input-container,
.button-container {
    margin-bottom: 15px; 
}

button {
    cursor: pointer; 
}
</style>
