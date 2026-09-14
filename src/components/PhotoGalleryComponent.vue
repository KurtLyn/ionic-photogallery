<template>
  <ion-card class="gallery-card">
    <ion-card-header>
      <div class="header-row">
        <ion-icon :icon="imagesIcon" class="header-icon" />
        <ion-card-title>Photo Gallery</ion-card-title>
      </div>
      <ion-card-subtitle v-if="photos.length">
        {{ photos.length }} {{ photos.length === 1 ? "photo" : "photos" }}
      </ion-card-subtitle>
    </ion-card-header>

    <ion-card-content>
      <div v-if="photos.length === 0" class="empty-gallery">
        <ion-icon :icon="imagesIcon" class="empty-icon" />
        <p class="empty-title">No pictures yet</p>
        <p class="empty-sub">Take a picture using the camera above.</p>
      </div>

      <ion-grid v-else class="gallery-grid">
        <ion-row>
          <ion-col
            v-for="(photo, index) in photos"
            :key="index"
            size="6"
            size-md="4"
          >
            <div class="photo-wrapper">
              <ion-img :src="photo" class="gallery-image" />
            </div>
          </ion-col>
        </ion-row>
      </ion-grid>
    </ion-card-content>
  </ion-card>
</template>

<script setup lang="ts">
import {
  IonCard,
  IonCardContent,
  IonCardHeader,
  IonCardSubtitle,
  IonCardTitle,
  IonCol,
  IonGrid,
  IonIcon,
  IonImg,
  IonRow,
} from "@ionic/vue";
import { images as imagesIcon } from "ionicons/icons";

defineProps<{ photos: string[] }>();
</script>

<style scoped>
.gallery-card {
  --background: #F5EFE6;
  border: 1px solid #e0d5c4;
  border-radius: 16px;
  box-shadow: 0 4px 16px rgba(62, 39, 35, 0.08);
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

/* Empty state */
.empty-gallery {
  text-align: center;
  padding: 40px 20px;
  color: #6D4C41;
}

.empty-icon {
  font-size: 56px;
  color: #C9A961;
  margin-bottom: 12px;
}

.empty-title {
  font-size: 1.05rem;
  font-weight: 600;
  color: #3E2723;
  margin: 4px 0;
}

.empty-sub {
  font-size: 0.85rem;
  color: #6D4C41;
  margin: 0;
}

/* Gallery */
.gallery-grid {
  padding: 0;
}

.photo-wrapper {
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 2px 10px rgba(62, 39, 35, 0.15);
  border: 2px solid #1B2A4A;
  background: #1B2A4A;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.photo-wrapper:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 16px rgba(27, 42, 74, 0.3);
}

.gallery-image {
  width: 100%;
  height: 160px;
  display: block;
}

.gallery-image::part(image) {
  object-fit: cover;
  width: 100%;
  height: 100%;
}
</style>