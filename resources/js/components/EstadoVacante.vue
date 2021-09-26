<template>
    <span
        class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full"
        :class="claseEstadoVacante()"
        @click="cambiarEstado"
        :key="estadoVacante"
    >
    {{ estadoVacanteText }}
    </span>
</template>
<script>
    export default {
        props:['estado', 'vacanteId'],
        mounted() {
            this.estadoVacante = Number(this.estado);
        },
        data: function() {
            return{
                estadoVacante: null
            }
        },
        methods: {
            claseEstadoVacante() {
                return this.estadoVacante === 1 ? "bg-green-200 text-green-800" : "bg-red-200 text-red-800"
            },
            cambiarEstado() {
                if (this.estadoVacante === 1) {
                    this.estadoVacante = 0;
                } else{
                    this.estadoVacante = 1;
                }
                /* Enviar a axios */
                const params = {
                    estado: this.estadoVacante
                }
                axios
                    .post('/vacantes/' + this.vacanteId, params)
                    .then(respuesta => console.log(respuesta))
                    .catch(error => console.log(error))
            }
        },
        computed: {
            estadoVacanteText(){
                return this.estadoVacante === 1 ? 'Activa' : 'Inactiva'
            }
        }
    }
</script>
