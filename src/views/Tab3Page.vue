<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Tab 3</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Tab 3</ion-title>
        </ion-toolbar>
      </ion-header>
      
      
      <div id="container">
        <p>Test form creation</p>
        <form @submit.prevent="handleSubmit">
          <ion-datetime presentation="date" size="cover" v-model="date"></ion-datetime>
          
          <ion-segment v-model="genre">
            <ion-segment-button value="action">
              <ion-label>Action</ion-label>
            </ion-segment-button>
            <ion-segment-button value="comedy">
              <ion-label>Comedy</ion-label>
            </ion-segment-button>
            <ion-segment-button value="horror">
              <ion-label>Horror</ion-label>
            </ion-segment-button>
            <ion-segment-button value="romance">
              <ion-label>Romance</ion-label>
            </ion-segment-button>
          </ion-segment>

          <ion-item>
            <ion-toggle v-model="toggle">
            </ion-toggle>
            <ion-label>Toggler</ion-label>
          </ion-item>

          <ion-button type="submit">Submit</ion-button>
        </form>
        <div v-if="submitted">
          <p>Date: {{date}}</p>
          <p>Genre: {{genre}}</p>
          <p>Toggled: {{toggle}}</p>
        </div>
      </div>

    </ion-content>
  </ion-page>
</template>

<script>
import { defineComponent } from 'vue';
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonDatetime, IonButton, IonLabel, IonSegment, IonSegmentButton, IonToggle} from '@ionic/vue';
export default defineComponent({
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage, IonDatetime, IonButton, IonLabel, IonSegment, IonSegmentButton, IonToggle},
  methods:{
    handleSubmit(){
      console.log(this.date)
      console.log(this.genre)
      console.log(this.toggle)
      this.submitted=true
    }
  },
  data(){
    return{
      date:'',
      genre:'',
      toggle:true,
      submitted:false
    }
  }

});
</script>

<style scoped>
#container {
  text-align: center;
  position: absolute;
  left: 0;
  right: 0;
  top: 10%;
}
</style>