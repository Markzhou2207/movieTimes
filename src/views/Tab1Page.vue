<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Current Movies</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Tab 1</ion-title>
        </ion-toolbar>
      </ion-header>
      <h1>  Currently showing movies</h1>
      

      <ion-item>
        <ion-label>Genre Filter</ion-label>
        <ion-select v-model="selectedGenre" interface="popover">
          <ion-select-option v-for="genre in genres" :key="genre.code" :value="genre.code">{{genre.name}}</ion-select-option>
          <ion-select-option value="none">Clear</ion-select-option>
        </ion-select>
      </ion-item>
      <ion-list>
        <ion-item v-for="movie in filteredMovie" :key="movie.Id">
            <ion-thumbnail slot="start">
              <img  v-bind:src="movie.LargePosterUrl" alt="not found" />
            </ion-thumbnail>
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
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent , IonList, IonItem, IonLabel, IonThumbnail, IonSelect, IonSelectOption } from '@ionic/vue';

export default defineComponent({
  name: 'Tab1Page',
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage, IonList, IonItem, IonLabel, IonThumbnail, IonSelect, IonSelectOption},
  data(){
    return{
      movies:[],
      genres:[],
      selectedGenre:"none",
    }
  },
  computed:{
    filteredMovie(){
      if( this.selectedGenre == "none"){
        return this.movies
      } else {
        return this.movies.filter(movie => movie.Genres == this.selectedGenre)
      }
    }
  },
  mounted(){
    fetch('http://localhost:8100/Movies/GetNowShowing')
      .then(response => response.json())
      .then(data => (this.movies=data.Data.Movies, this.genres=data.Data.Genres))
  }
});
</script>
