<template>
    <div>
        <form @submit.prevent="agregar">
            <ion-item>
                <ion-label position="floating">Nombre</ion-label>
                <ion-input class="form-control" :value="nombre" @input= "nombre = $event.target.value"></ion-input>
            </ion-item>

            <ion-item>
                <ion-label position="floating">IP Local</ion-label>
                <ion-input class="form-control" :value="ipLocal" @input= "ipLocal = $event.target.value"></ion-input>
            </ion-item>

            <ion-item>
                <ion-label position="floating">IP Remota</ion-label>
                <ion-input class="form-control" :value="ipRemota" @input= "ipRemota = $event.target.value"></ion-input>
            </ion-item>

            <ion-card-content>
                <ion-button type="submit" expand="block">Agregar</ion-button>
            </ion-card-content>
            
            <ion-card>
                <ion-card-header>
                    <ion-card-subtitle>Molinos</ion-card-subtitle>
                </ion-card-header>

                <ion-card-content>
                    <ion-list>
                        <ion-item v-for="molino of molinos" v-bind:key="molino.ipLocal">
                            <ion-label>{{molino.nombre}}</ion-label>
                            <ion-label size="small">{{molino.ipLocal}}</ion-label>
                            <ion-button size="small" color="danger" @click="eliminar(molino.ipLocal)">Eliminar</ion-button>
                        </ion-item>
                    </ion-list>
                </ion-card-content>
            </ion-card>
        </form>
    </div>
</template>
<script lang="ts">
    export default {
        data(){
            return{
                molinos: [],
                nombre: '',
                ipLocal: '',
                ipRemota: '',

            }
        },
        created(){
            let datosDB= JSON.parse(localStorage.getItem('molinos'));
            if(datosDB === null){
                this.molinos = [];
            }else{
                this.molinos = datosDB;
            }
        },
        methods:{
            agregar(){
                this.molinos.push({
                    nombre: this.nombre,
                    ipLocal: this.ipLocal,
                    ipRemota: this.ipRemota,
                });
                this.nombre= '';
                this.ipLocal= '';
                this.ipRemota= '';
                localStorage.setItem('molinos', JSON.stringify(this.molinos));
            },
            eliminar(index){
                this.molinos.splice(index, 1);
                localStorage.setItem('molinos', JSON.stringify(this.molinos));
            }
        }
    }
</script>