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
      <div id='page-title'>
        <h1>  Currently showing movies</h1>
      </div>

      <ion-item>
        <ion-label>Genre Filter</ion-label>
        <ion-select v-model="selectedGenre" interface="popover">
          <ion-select-option v-for="genre in genres" :key="genre.code" :value="genre.code">{{genre.name}}</ion-select-option>
          <ion-select-option value="none">Clear</ion-select-option>
        </ion-select>
      </ion-item>
      <ion-list>
        <ion-item v-for="movie in filteredMovie" :key="movie.Id" v-on:click='openModal(movie)'>
            <ion-thumbnail slot="start">
              <img  v-bind:src="movie.LargePosterUrl" alt="not found" />
            </ion-thumbnail>
            <ion-label>
              <!-- <router-link :to="{ name: 'movieInfo', params: { movieInfo: movie, name:movie.Name, genre: movie.Genres, poster: movie.LargePosterUrl }}"><h2>{{movie.Name}}</h2></router-link> -->
              <h2>{{movie.Name}}</h2>
              <h3>{{movie.Director}}</h3>
              <p>{{movie.Genres}}</p>
            </ion-label>
        </ion-item>
      </ion-list>
      <InformationModal :isVisible="this.modalVisible" v-bind:info="this.selectedMovie" @cancel='closeModal()'/>

    </ion-content>
  </ion-page>
</template>

<script>
import { defineComponent } from 'vue';
import InformationModal from '@/components/InformationModal.vue';
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent , IonList, IonItem, IonLabel, IonThumbnail, IonSelect, IonSelectOption } from '@ionic/vue';

export default defineComponent({
  name: 'Tab1Page',
  components: { InformationModal, IonHeader, IonToolbar, IonTitle, IonContent, IonPage, IonList, IonItem, IonLabel, IonThumbnail, IonSelect, IonSelectOption},
  data(){
    return{
      movies:[],
      genres:[],
      selectedGenre:"none",
      modalVisible:false,
      selectedMovie:""
    }
  },
  methods:{
    openModal(movie){
      this.selectedMovie=movie;
      this.modalVisible=true;
      console.log(this.modalVisible)
    },
    closeModal(){
      this.modalVisible=false;

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


<style scoped>
p {
  text-transform: capitalize;
}
#page-title{
  text-align: center;
}
</style>