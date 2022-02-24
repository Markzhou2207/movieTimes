<template>
  <div>
  <ion-modal
    :is-open=this.isVisible>
            
            <ion-content>
              <div id='page-title'>
                <ion-button id="close-modal" @click="emitCancel">Close</ion-button>
                <h1>{{this.info.Name}}</h1>
              </div>

              <div id='info-body'>
                <ion-img v-bind:src="this.info.LargePosterUrl" alt='Poster Not Found'></ion-img>
                <div>
                  <h3>Genre: {{this.info.Genres}}</h3>
                  <h3>Director : {{this.info.Director}} min</h3>
                  <h3>Run Time: {{this.info.RunningTime}} min</h3>
                  <h3>Release Date : {{this.info.ReleasedAt}} </h3>
                  <h3>Cast : {{this.info.MainCast}} </h3>
                  <h3>Synopsis :</h3>
                  <p>{{this.info.Synopsis}}</p>
                </div>
              </div>
            </ion-content>
  </ion-modal>
  </div>
</template>

<script>

import { defineComponent } from 'vue';
import { IonModal, IonButton, IonContent, IonImg} from '@ionic/vue';
export default defineComponent({
    components: {  IonModal, IonButton, IonContent, IonImg },

  name: 'InformationModal',
  props: {
    isVisible:{
      required: true,
    },
    info:{
      required: true,
    },
  },
  methods:{
    emitCancel(){
      this.$emit('cancel')
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
.datetime-calendar{
  text-align: center;
  position: absolute;
  left: 0;
  right: 0;
  top: 5em;
}
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
#close-modal{
  float:right;
}
ion-img{
  height:550px;
  width:auto;
  align-items: center;
}
</style>