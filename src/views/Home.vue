<template>
  <div class="home">
    <ion-card>
      <ion-card-header>
        <ion-card-title>Estado Actual</ion-card-title>
      </ion-card-header>

      <ion-card-content>
        <ion-item>
          <ion-label>Conexion</ion-label>
          <ion-select placeholder="Seleccione" :value="conexion_local" @ionChange="conexion_local= $event.target.value">
            <ion-select-option value= "local">Local </ion-select-option>
            <ion-select-option value= "remota">Remota </ion-select-option>
          </ion-select>   
        </ion-item>
      </ion-card-content>
    </ion-card>

    <ion-card v-if="cargando">
      <ion-card-content class="contenedor">
        <ion-item class="preloader" >
        </ion-item>
      </ion-card-content>
    </ion-card>
    <Molino v-for="(molino, index) of estadosMolinos" :key="index" :nombre='molino.nombre' :data='molino.data'  />
  </div>
</template>

<script>
// @ is an alias to /src
import axios from 'axios';
import Molino from '@/components/Molino.vue'

export default {
  components: {
    Molino
  },
  data: function(){
      return{
        cargando: true,
        intervalo: 20000,
        molinios: [],
        estadosMolinos: [],
        conexion_local: "local",
      }
    },
    mounted(){
      let datosDB= JSON.parse(localStorage.getItem('molinos'));
      if(datosDB === null){
        this.molinos = [];
      }else{
        this.molinos = datosDB;
      }
      this.getEstados();
    },
    methods:{
      getEstados() {
        setInterval(() => {
          this.estadosMolinos= [];
          if(this.conexion_local === "local"){
            for (const molino of this.molinos) {
              this.getMolino('http://'+molino.ipLocal, molino.nombre);
            }
          }
          if(this.conexion_local === "remota"){
            for (const molino of this.molinos) {
              this.getMolino('http://'+molino.ipRemota, molino.nombre);
            }
          }
        }, this.intervalo);
      },
      async getMolino (url, nombre) { 
        await axios.get(url).then(response=>{
          this.estadosMolinos.push({'nombre': nombre, 'data': response.data});
          this.cargando= false; 
          console.log(this.conexion_local);
        }).catch(() => {
          alert("No se puede conectar al Servidor, Verifique su conexion!")
      });
      },
    }
}
</script>