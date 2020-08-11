<template>
  <ion-app id="app">
    <ion-toolbar color="dark">
      <ion-buttons slot="secondary">
        <ion-button>
          <router-link to="/"><ion-icon name="home"></ion-icon></router-link> 
        </ion-button>
      </ion-buttons>
      <ion-buttons slot="primary">
        <ion-button color="danger">
          <router-link to="/configuracion"><ion-icon name="settings"></ion-icon></router-link>     
        </ion-button>
      </ion-buttons>
      <ion-title>Water Status</ion-title>
    </ion-toolbar>
    <ion-content>
      <router-view/>
    </ion-content>
  </ion-app>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

/* #nav a.router-link-exact-active {
  color: #42b983;
} */
</style>
