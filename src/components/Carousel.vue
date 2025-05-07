<script setup lang="ts">
  import { ref } from 'vue';

  interface Props {
    images: string[];
  }

  const props = defineProps<Props>();

  const selectedImage = ref<string>(props.images[0]);

  function selectImage(image: string) {
    if (image === selectedImage.value) return;
    selectedImage.value = image;
  }
</script>

<template>
  <div class="carousel">
    <img :src="selectedImage" :key="selectedImage" alt="Selected image" class="carousel__main-image" />

    <div class="carousel__thumbnails">
      <img v-for="img in images" :key="img" :src="img" alt="Thumbnail" :class="[
        'carousel__thumbnail',
        { 'carousel__thumbnail--active': selectedImage === img }
      ]" @click="selectImage(img)" />
    </div>
  </div>
</template>

<style scoped>
.carousel {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-6);
}

.carousel__main-image {
  width: 100%;
  aspect-ratio: 1 / 1;
  border-radius: var(--radius-medium);
  object-fit: cover;
  opacity: 0;
  transform: scale(0.97);
  animation: fadeInScale 3s cubic-bezier(0.33, 1, 0.68, 1) forwards;
}

@keyframes fadeInScale {
  to {
    opacity: 1;
    transform: scale(1);
  }
}

.carousel__thumbnails {
  display: flex;
  gap: var(--spacing-4);
}

.carousel__thumbnail {
  width: 64px;
  height: 64px;
  border-radius: var(--radius-small);
  border: 2px solid transparent;
  cursor: pointer;
  object-fit: cover;
  transition: transform 0.2s ease;

  &:hover {
    transform: scale(1.05);
  }
}

.carousel__thumbnail--active {
  border-color: var(--brand-border, var(--purple-500));
}
</style>
