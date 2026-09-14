<template>
  <ion-card class="camera-card">
    <ion-card-header>
      <div class="header-row">
        <ion-icon :icon="cameraIcon" class="header-icon" />
        <ion-card-title>Camera</ion-card-title>
      </div>
      <ion-card-subtitle>Snap a new memory</ion-card-subtitle>
    </ion-card-header>

    <ion-card-content>
      <ion-button expand="block" @click="takePicture" class="capture-btn">
        <ion-icon slot="start" :icon="cameraIcon" />
        Take Picture
      </ion-button>

      <ion-text v-if="errorMessage" color="danger">
        <p class="error-text">{{ errorMessage }}</p>
      </ion-text>
    </ion-card-content>
  </ion-card>
</template>

<script setup lang="ts">
import {
  IonButton,
  IonCard,
  IonCardContent,
  IonCardHeader,
  IonCardSubtitle,
  IonCardTitle,
  IonIcon,
  IonText,
} from "@ionic/vue";
import { camera as cameraIcon } from "ionicons/icons";
import { Camera } from "@capacitor/camera";
import { ref } from "vue";

const errorMessage = ref("");
const emit = defineEmits<{ (event: "photoCaptured", photo: string): void }>();

const takePicture = async () => {
  errorMessage.value = "";
  try {
    const photo = await Camera.takePhoto({ quality: 90, saveToGallery: false });
    if (photo.webPath) {
      emit("photoCaptured", photo.webPath);
    }
  } catch (error) {
    console.error(error);
    errorMessage.value = "Unable to capture photo.";
  }
};
</script>

<style scoped>
.camera-card {
  --background: #F5EFE6;
  border: 1px solid #e0d5c4;
  border-radius: 16px;
  box-shadow: 0 4px 16px rgba(62, 39, 35, 0.08);
  margin-bottom: 20px;
}

.header-row {
  display: flex;
  align-items: center;
  gap: 10px;
}

.header-icon {
  font-size: 24px;
  color: #1B2A4A;
}

ion-card-title {
  color: #3E2723;
  font-weight: 700;
  font-size: 1.25rem;
}

ion-card-subtitle {
  color: #6D4C41;
  font-size: 0.85rem;
  margin-top: 4px;
  letter-spacing: 0.3px;
}

.capture-btn {
  --background: #1B2A4A;
  --background-hover: #32405c;
  --background-activated: #182541;
  --color: #F5EFE6;
  --border-radius: 12px;
  --box-shadow: 0 4px 12px rgba(27, 42, 74, 0.25);
  font-weight: 600;
  letter-spacing: 0.5px;
  height: 48px;
  text-transform: none;
}

.error-text {
  margin-top: 12px;
  text-align: center;
  font-size: 0.85rem;
}
</style>