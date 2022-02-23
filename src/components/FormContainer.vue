<template>
  <div id="container">
    <strong>{{ name }}</strong>
    <p>Test form creation</p>
    <ion-datetime presentation="date" size="cover" value="{{today}}"></ion-datetime>
  </div>
</template>

<script>

import { defineComponent } from 'vue';

export default defineComponent({
  name: 'FormContainer',
  props: {
    name: String
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
</style>