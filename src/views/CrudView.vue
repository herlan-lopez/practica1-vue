<template>
    <div class="about mx-5">
        <h3 class="mb-3 mt-3 text-center text-primary"><b>CONTACTOS</b></h3>
        <div>


            <div class="mb-4">
                <div class="input-group">
                    <span class="input-group-text bg-dark text-white" id="description-search-text">
                        <i class="bi bi-search"></i> &nbsp;&nbsp;<b>Buscar por cualquier campo</b>
                    </span>
                    <input type="search" class="form-control" id="description-search" placeholder="escriba"
                        @input="toSearch = $event.target.value">
                </div>
            </div>

            <div class="mb-3">
                <div class="input-group">
                    <span class="input-group-text bg-dark text-white" id="type-filter">
                        <i class="bi bi-filter"></i> &nbsp;&nbsp;<b> Filtrar por nombre</b>
                    </span>
                    <select class="form-select" @change="toFilter = $event.target.value">
                        <option value="">todos</option>
                        <option v-for="nombre in types" :value="nombre" :key="nombre">{{ nombre }}</option>
                    </select>
                </div>
            </div>




            

        </div>

        <div class="card">
            <div class="card-body">
                <form @submit.prevent="save()">
                    <table class="table table-striped table-bordered border-primary">
                        <thead class="table-primary">
                            <tr>
                                <th colspan="1">



                                </th>
                                <th>
                                    <input type="text" class="form-control" id="nombre" placeholder="nombre"
                                        v-model="nuevoContacto.nombre">
                                </th>
                                <th>
                                    <input type="email" class="form-control" id="correo" placeholder="correo"
                                        v-model="nuevoContacto.correo">
                                </th>
                                <th>
                                    <input type="text" class="form-control" id="direccion" placeholder="direccion"
                                        v-model="nuevoContacto.direccion">
                                </th>
                                <th>
                                    <input type="number" class="form-control" id="telefono" placeholder="telefono"
                                        v-model="nuevoContacto.telefono">
                                </th>
                                <th>
                                    <input type="text" class="form-control" id="pais" placeholder="pais"
                                        v-model="nuevoContacto.pais">
                                </th>
                                <th>
                                    <input type="text" class="form-control" id="ciudad" placeholder="ciudad"
                                        v-model="nuevoContacto.ciudad">
                                </th>
                                <th>
                                    <button type="submit" class="btn btn-primary">Agregar</button>
                                </th>
                            </tr>
                            <tr>
                                <th scope="col" class="text-center" style="background: blue;color:white">id</th>
                                <th scope="col" class="text-center" style="background: blue;color:white">Nombre</th>
                                <th scope="col" class="text-center" style="background: blue;color:white">Correo</th>
                                <th scope="col" class="text-center" style="background: blue;color:white">Direccion</th>
                                <th scope="col" class="text-center" style="background: blue;color:white">Telefono</th>
                                <th scope="col" class="text-center" style="background: blue;color:white">Pais</th>
                                <th scope="col" class="text-center" style="background: blue;color:white">Ciudad</th>
                                <th style="background: blue;"></th>
                            </tr>
                        </thead>

                        <tbody>
                            <tr v-for="(link, index) in getList()" :key="index">
                                <th scope="row">{{ link.id }}</th>
                                <td>{{ link.nombre }}</td>
                                <td>{{ link.correo }}</td>
                                <td>{{ link.direccion }}</td>
                                <td>{{ link.telefono }}</td>
                                <td>{{ link.pais }}</td>
                                <td>{{ link.ciudad }}</td>


                                <td class="text-center">
                                    <button type="button" class="btn btn-success btn-sm" @click="edit(index)"><i
                                            class="bi bi-pencil-square"></i></button>

                                    <button type="button" class="btn btn-danger btn-sm" @click="remove(index)"><i
                                            class="bi bi-trash3"></i></button>
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </form>
            </div>
        </div>

        <!-- Modal -->
        <div class="modal fade" id="editModal" tabindex="-1" aria-labelledby="editModalLabel" aria-hidden="true">
            <div class="modal-dialog modal-xl">
                <div class="modal-content">
                    <div class="modal-header text-center bg-success text-white">
                        <h1 class="modal-title fs-5 text-white" id="editModalLabel">Editar</h1>
                        <button type="button" class="btn-close text-white" data-bs-dismiss="modal"
                            aria-label="Close"></button>
                    </div>
                    <form @submit.prevent="saveEdit()">
                        <div class="modal-body" v-if="itemSelected">
                            <div class="row">
                             
                                <div class="col-md-6 mb-3">
                                    <label for="updateDescription" class="form-label fw-bold">Nombre</label>
                                    <input type="text" v-model="itemSelected.nombre" class="form-control"
                                        id="updateDescription" required>
                                </div>
                                <div class="col-md-6 mb-3">
                                    <label for="updateDescription" class="form-label fw-bold">Correo</label>
                                    <input type="email" v-model="itemSelected.correo" class="form-control"
                                        id="updateDescription" required>
                                </div>

                           
                                <div class="col-md-6 mb-3">
                                    <label for="updateDescription" class="form-label fw-bold">Direccion</label>
                                    <input type="text" v-model="itemSelected.direccion" class="form-control"
                                        id="updateDescription" required>
                                </div>
                                <div class="col-md-6 mb-3">
                                    <label for="updateDescription" class="form-label fw-bold">Telefono</label>
                                    <input type="number" v-model="itemSelected.telefono" class="form-control"
                                        id="updateDescription" required>
                                </div>

                            
                                <div class="col-md-6 mb-3">
                                    <label for="updateDescription" class="form-label fw-bold">Pais</label>
                                    <input type="text" v-model="itemSelected.pais" class="form-control"
                                        id="updateDescription" required>
                                </div>
                                <div class="col-md-6 mb-3">
                                    <label for="updateDescription" class="form-label fw-bold">Ciudad</label>
                                    <input type="text" v-model="itemSelected.ciudad" class="form-control"
                                        id="updateDescription" required>
                                </div>
                            </div>
                        </div>

                        <div class="modal-footer">
                            <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cancelar</button>
                            <button type="submit" class="btn btn-primary"><i class="bi bi-pencil-square"></i>
                                Editar</button>
                        </div>
                    </form>

                </div>
            </div>
        </div>

    </div>
</template>

<script>
export default {
    data() {
        return {
            types: [],
            nuevoContacto: {
                id:'',
                nombre: '',
                correo: '',
                direccion: '',
                telefono: '',
                pais: '',
                ciudad: ''
            },

            contactoArray: [
                {
                    id:'1',
                    nombre: 'HERLAN LOPEZ',
                    correo: 'halael.rey@gmail.com',
                    direccion: 'CALLE C ENTRE 5 Y 6',
                    telefono: '67155712',
                    pais: 'BOLIVIA',
                    ciudad: 'ORURO'
                },
                {
                    id:'2',
                    nombre: 'LENNY MENDOZA ',
                    correo: 'lenny@gmail.com',
                    direccion: 'CATAVI',
                    telefono: '67757575',
                    pais: 'BOLIVIA',
                    ciudad: 'LLALLAGUA'
                },
                {
                    id:'3',
                    nombre: 'JUAN PEREZ ',
                    correo: 'perez@hotmail.com',
                    direccion: 'CALLE BOLIVAR',
                    telefono: '67867876',
                    pais: 'BOLIVIA',
                    ciudad: 'LA PAZ'
                },

            ],
            itemSelected: null,
            indexSelected: null,
            typeFilter: '',
            toFilter: '',
            toSearch: ''
        }
    },
    mounted() {
     
        this.types = [...new Set(this.contactoArray.map(item => item.nombre))];
    },
    methods: {


        updateTypes() {
        
            this.types = [...new Set(this.contactoArray.map((item) => item.nombre))];
        },
        filterLinksByName() {
            const searchTerm = this.toSearch.toLowerCase().trim(); 
            this.filteredLinks = this.contactoArray.filter(link =>
                link.nombre.toLowerCase().includes(searchTerm)
            );
        },
        save() {

    if (this.nuevoContacto.nombre && this.nuevoContacto.correo && this.nuevoContacto.direccion && this.nuevoContacto.telefono && this.nuevoContacto.pais && this.nuevoContacto.ciudad) {
        

        this.nuevoContacto.nombre = this.nuevoContacto.nombre.toUpperCase();
        this.nuevoContacto.direccion = this.nuevoContacto.direccion.toUpperCase();
        this.nuevoContacto.pais = this.nuevoContacto.pais.toUpperCase();
        this.nuevoContacto.ciudad = this.nuevoContacto.ciudad.toUpperCase();


     
        const lastId = this.contactoArray.length > 0 ? Math.max(...this.contactoArray.map(link => parseInt(link.id))) : 0;
        this.nuevoContacto.id = (lastId + 1).toString(); 

       
        this.contactoArray.push({ ...this.nuevoContacto });

    
        if (!this.types.includes(this.nuevoContacto.nombre)) {
            this.types.push(this.nuevoContacto.nombre);
        }

    
        this.nuevoContacto = {
            id: '',
            nombre: '',
            correo: '',
            direccion: '',
            telefono: '',
            pais: '',
            ciudad: ''
        };

        Swal.fire({
            icon: 'success',
            title: 'AGREGADO',
            text: 'Contacto se ha añadido correctamente.',
            color: '#fff',
            confirmButtonText: 'OK'
        });
    } else {
        Swal.fire({
            icon: 'warning', 
            title: 'Campos incompletos',
            text: 'Por favor, completa todos los campos.',
            color: '#fff',
            confirmButtonText: 'Entendido',
        });
    }
},

        remove(index) {
            const contactName = this.contactoArray[index].nombre;
         
            Swal.fire({
                title: '¿Estás seguro de Eliminar?',
                text: `El contacto ${contactName} será eliminado.`,
                color: '#fff',
                icon: 'warning',
                showCancelButton: true,
                confirmButtonText: 'Sí, eliminar',
                cancelButtonText: 'Cancelar',
                reverseButtons: false
            }).then((result) => {
                if (result.isConfirmed) {
                    this.contactoArray.splice(index, 1);
                    this.updateTypes();

                    Swal.fire({
                        icon: 'success',
                        title: 'Eliminado',
                        text: 'El contacto ha sido eliminado correctamente.',
                        color: '#fff',
                        confirmButtonText: 'OK',
                    });
                }
            });
        }
        ,
        edit(index) {
            this.itemSelected = { ...this.contactoArray[index] };
            this.indexSelected = index;
            const editModal = new bootstrap.Modal(document.getElementById('editModal'));
            editModal.show();
        },
        saveEdit() {
            this.contactoArray[this.indexSelected] = { ...this.itemSelected };

            this.updateTypes();

            const modalElement = document.getElementById('editModal');
            const modalInstance = bootstrap.Modal.getInstance(modalElement) || new bootstrap.Modal(modalElement);
            modalInstance.hide();

            this.itemSelected = null;
            this.indexSelected = null;

            Swal.fire({
                icon: 'success',
                title: 'Editado',
                text: 'Contacto se ha editado correctamente.',
                color: '#fff',
                confirmButtonText: 'OK'
            });
        },
        getList() {

            const searchTerm = this.toSearch.toLowerCase().trim();
            const selectedName = this.toFilter;

            return this.contactoArray.filter((item) => {

             const matchesSearch = searchTerm
                    ? item.nombre.toLowerCase().includes(searchTerm) ||
                    item.correo.toLowerCase().includes(searchTerm) ||
                    item.direccion.toLowerCase().includes(searchTerm)||
                    item.id.includes(searchTerm)||
                    item.telefono.includes(searchTerm)||
                    item.pais.toLowerCase().includes(searchTerm)||
                    item.ciudad.toLowerCase().includes(searchTerm)
                    
                    : true;


                const matchesFilter = selectedName ? item.nombre === selectedName : true;

                return matchesSearch && matchesFilter;
            });
        }


    }
}
</script>

<style>
.btn {
    margin-right: 3px;
}

.card {
    overflow-x: auto;
}
</style>
