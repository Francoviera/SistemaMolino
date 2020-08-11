<template>
    <ion-card>
        <ion-card-header>
            <ion-card-title>{{nombre}}</ion-card-title>
        </ion-card-header>
        
        <ion-card-content>
            <h4 class="porcentaje">Capacidad: <ion-text v-if="porcentaje<=20" color="danger">{{porcentaje}}%</ion-text><ion-text v-else color="success">{{porcentaje}}%</ion-text>  Bomba: <ion-text v-if="data.bomba === false" color="danger">Apagada</ion-text><ion-text v-else color="success">Encendida</ion-text></h4>
            <ion-item class="container">
            </ion-item>
        </ion-card-content>
    </ion-card>
</template>
<script>
    
    export default {
        props:['nombre', 'data'],
         data: function(){
            return{
                porcentaje: 0,
            }
        },
        mounted(){
            if(this.data.alto >50){
                document.querySelector(".container").style.setProperty('--liquid', 100+"%");
                this.porcentaje= 100;
            }else if(this.data.medio >50){
                document.querySelector(".container").style.setProperty('--liquid', 50+"%");
                this.porcentaje= 50;
            }else if(this.data.bajo >50){
                document.querySelector(".container").style.setProperty('--liquid', 20+"%");
                this.porcentaje= 20;
            }else{
                document.querySelector(".container").style.setProperty('--liquid', 0+"%");
                this.porcentaje= 0;
            }
        },
    }
</script>