<template>
  <ion-page>
    <ion-header class="ion-no-border">
      <ion-toolbar class="app-toolbar">
        <ion-title>My Photo Gallery</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content class="ion-padding app-content">
      <CameraComponent @photo-captured="addPhoto" />
      <PhotoGalleryComponent :photos="photos" />
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import {
  IonContent,
  IonHeader,
  IonPage,
  IonTitle,
  IonToolbar,
} from "@ionic/vue";
import { ref } from "vue";
import CameraComponent from "@/components/CameraComponent.vue";
import PhotoGalleryComponent from "@/components/PhotoGalleryComponent.vue";

const photos = ref<string[]>([]);

const addPhoto = (photo: string) => {
  photos.value.unshift(photo);
};
</script>

<style scoped>
.app-toolbar {
  --background: #1B2A4A;
  --color: #F5EFE6;
  --min-height: 60px;
  box-shadow: 0 2px 12px rgba(27, 42, 74, 0.25);
}

ion-title {
  font-weight: 700;
  letter-spacing: 0.5px;
  font-size: 1.15rem;
  color: #F5EFE6;
}

.app-content {
  --background: #FAF6F0;
}
</style>