<template>
  <div class="card">
       <div class="card-header text-primary" style="background: #e9ecef;"><small>Publicado el {{nota.created_at}} - Ultima actualización {{nota.updated_at}}</small></div>

        <div class="card-body">
             <input v-if="editMode" type="text" class="form-control" v-model="nota.descripcion">
            <p v-else>{{nota.descripcion}}</p>      
        </div>

        <div class="card-footer">
            <button v-if="editMode" class="btn btn-success btn-block" style="max-width: 18rem; margin: 0 auto;" @click="onClickUpdate()">Guardar cambios</button>
            <button v-else class="btn btn-secondary" @click="onClickEdit()">Editar nota</button>
            <button v-if="editMode" style="display: none" class="btn btn-danger" @click="onClickDelete()">Eliminar nota</button>
            <button v-else class="btn btn-danger" @click="onClickDelete()">Eliminar nota</button>
        </div>
    </div>
</template>

<script>
    export default {

        props: ['nota'],

        data () {
            return {
                editMode: false
            };

        },
        mounted() {
            console.log('Component mounted.')
        },

        methods: {

            onClickDelete(){
                axios.delete(`/notas/${this.nota.id}`)
                
                .then(() => {

                      this.$emit('delete');

                });
              
            },

            onClickEdit(){
               this.editMode = true;
            },

            onClickUpdate(){

                const params = {

                    descripcion: this.nota.descripcion

                };

                axios.put(`/notas/${this.nota.id}`, params)
                
                .then((response) => {
                    
                    this.editMode = false;
                    const nota = response.data;
                    this.$emit('update', nota);

                });

            }

        }
    }
</script>
