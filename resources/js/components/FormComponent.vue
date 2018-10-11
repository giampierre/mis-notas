<template>
         <div class="card text-center">
                <div class="card-header" style="background: #128c7e; color: #fff;">Agregar notas para añadir a la lista</div>

                <div class="card-body">          
                    <form action="" v-on:submit.prevent="newNota()">
                            <div class="form-group">
                            <label for="notas"></label>
                            <input type="text" class="form-control" cols="20" rows="0" name="notas" v-model="descripcion" placeholder="Escribe una nota...">
                            </div>
                            <button type="submit" class="btn btn-primary btn-block" style="max-width: 18rem; margin: 0 auto;">Registrar nota</button>
                    </form>
                </div>
            </div>
            
</template>

<script>
    export default {
        data() {
            return {
                descripcion: ''
            };
        },
        mounted() {
            console.log('Component mounted.')
        },
        methods: {

            newNota(){

                if (this.descripcion.length <= 1) return alert("Ingrese una nota");

                const params = {
                    descripcion: this.descripcion
                };

                this.descripcion = '';

                axios.post('/notas', params)
                .then((response) => {

                    const nota = response.data;
                    this.$emit('new', nota); 
                    
                     console.log(response);

                });

               

            }

        }
    }
</script>
