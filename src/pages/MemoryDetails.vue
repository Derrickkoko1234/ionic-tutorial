<template>
  <base-layout
    :page-title="loadedMemory ? loadedMemory.title : 'Loading'"
    page-default-back-link="/memories"
  >
    <h2 v-if="!loadedMemory">Could not find a memory for the given id.</h2>
    <ion-card v-else>
      <ion-card-header>
        <ion-card-title>{{ loadedMemory.title }}</ion-card-title>
      </ion-card-header>
      <ion-card-content>
        <ion-img :src="loadedMemory.image"></ion-img>
        <p>{{ loadedMemory.description }}</p>
      </ion-card-content>
    </ion-card>
  </base-layout>
</template>
<script>
import {
  IonCard,
  IonCardHeader,
  IonCardTitle,
  IonCardContent,
  IonImg,
} from "@ionic/vue";
export default {
  components: {
    IonCard,
    IonCardHeader,
    IonCardTitle,
    IonCardContent,
    IonImg,
  },
  data() {
    return {
      memoryId: this.$route.params.id,
    };
  },
  computed: {
    loadedMemory() {
      return this.$store.getters.memory(this.memoryId);
    },
  },
  watch: {
    $route(currentRoute) {
      this.memoryId = currentRoute.params.id;
    },
  },
};
</script>
