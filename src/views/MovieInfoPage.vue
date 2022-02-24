<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Movie Details</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Tab 2</ion-title>
        </ion-toolbar>
      </ion-header>
      <div id='page-title'>
        <h1>{{this.name}}</h1>
      </div>

      <div id='info-body'>
        <ion-img v-bind:src="poster" alt='Poster Not Found'></ion-img>
        <div>
          <h3>Genre: {{this.genre}}</h3>
          <h3>Movie Info: {{this.movieInfo.Name}}</h3>
        </div>
      </div>
      
      
    </ion-content>
  </ion-page>
</template>

<script>
import { defineComponent } from 'vue';
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonImg } from '@ionic/vue';

export default defineComponent({
  name: 'MovieInfoPage',
   props:{
    movieInfo:{
      required: true
    },

    name:{
      required: true,
      default: null
    },
    genre:{
      required:true,
      default:''
    },
    poster:{
      required:true,
      default:''
    }
  }, 
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage, IonImg }
});
</script>



<style scoped>
h1{
  font-weight: bold;
}
h3 {
  text-transform: capitalize;
}
#page-title{
  text-align: center;
}
#info-body{
  text-align: center;
}
ion-img{
  height:550px;
  width:auto;
  align-items: center;
}
</style>