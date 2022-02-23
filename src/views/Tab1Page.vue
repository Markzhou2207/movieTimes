<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Tab 1</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Tab 1</ion-title>
        </ion-toolbar>
      </ion-header>
      <h1>  Currently showing movies</h1>
      <ion-list>
        <ion-item v-for="movie in movies" :key="movie.Id">
            <ion-label>
              <h2>{{movie.Name}}</h2>
              <h3>{{movie.Director}}</h3>
              <p>{{movie.Genres}}</p>
            </ion-label>
        </ion-item>
      </ion-list>
    </ion-content>
  </ion-page>
</template>

<script>
import { defineComponent } from 'vue';
// import axios from 'axios';
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent , IonList, IonItem, IonLabel } from '@ionic/vue';

export default defineComponent({
  name: 'Tab1Page',
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage, IonList, IonItem, IonLabel},
  data(){
    return{
      movies:[],
    }
  },
  mounted(){
    // fetch('https://localhost:8100/Movies/GetNowShowing')
    // .then(res=>res.json())
    // .then((res)=>console.log(res))
    //  https://www.eventcinemas.com.au/Movies/GetNowShowing
    // .catch(err=>console.log("ERROR - "+err.message))
    // axios.get('https://localhost:8100/Movies/GetNowShowing');
    fetch('http://localhost:8100/Movies/GetNowShowing')
      .then(response => response.json())
      .then(data => (this.movies=data.Data.Movies))
  }
});
</script>
