<template>
   <div class="row justify-content-center">
        <div class="col-md-8">

            <form-component @new="addNota"></form-component>
            <br>
            <notas-component class="mb-3" v-for="(nota, index) in notas" :key="nota.id" :nota="nota" @update="updateNota(index, ...arguments)" @delete="deleteNota(index)"></notas-component>      
        
        </div>
    </div>
</template>

<script>
    export default {
        data (){

            return {
                notas: []
            };

        },
        mounted() {
            axios.get('/notas')
            .then((response)=> {

                this.notas = response.data;
                
            });
        },

        methods: {
            addNota(nota){
                this.notas.push(nota);
            },
             updateNota(index, nota){
                this.notas[index] = nota;
            },
            deleteNota(index){
                this.notas.splice(index, 1);
            }
        }
    }
</script>
