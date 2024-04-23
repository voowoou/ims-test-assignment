<template>
  <div class="gallery">
    <div v-for="img in imgs" :key="img.id" @click="openModal(img)" class="image-container">
      <CustomImage :src="img.webformatURL" :alt="img.tags" class="image" />
      <ImageStats :likes="img.likes" :views="img.views" />
    </div>
    <ImageModal
      v-if="modalOpen"
      :src="clickedImgData.src"
      :alt="clickedImgData.alt"
      :likes="clickedImgData.likes"
      :views="clickedImgData.views"
      @close="modalOpen = false"
    />
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';
import CustomImage from './components/UI/CustomImage.vue';
import ImageStats from './components/UI/ImageStats.vue';
import ImageModal from './components/UI/ImageModal.vue';

export default {
  components: { CustomImage, ImageStats, ImageModal },
  setup() {
    const imgs = ref([]);
    const modalOpen = ref(false); // Флаг состояния модального окна с картинкой на весь экран
    const clickedImgData = ref({ src: '', alt: '', likes: 0, views: 0 }); // Объект с информацией о картинке, по к-рой кликнули

    const fetchPictures = async () => {
      const accessKey = '43519975-c4223c9989f17a91776b057d1';
      const endPoint = `https://pixabay.com/api/?key=${accessKey}&per_page=20`;

      try {
        const response = await fetch(endPoint);
        const imgsObj = await response.json();
        imgs.value = imgsObj.hits;
      } catch (error) {
        alert('Возникла ошибка при загрузке: ' + error);
      }
    };

    onMounted(fetchPictures);

    const openModal = img => {
      clickedImgData.value.src = img.webformatURL;
      clickedImgData.value.alt = img.tags;
      clickedImgData.value.likes = img.likes;
      clickedImgData.value.views = img.views;
      modalOpen.value = true;
    };

    return {
      imgs,
      modalOpen,
      clickedImgData,
      openModal,
    };
  },
};
</script>

<style>
.gallery {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1vw;
}

.image-container {
  display: flex;
  flex-direction: column;
}

.image {
  background: #828282;
  height: 200px;
}

@media only screen and (max-width: 768px) {
  .gallery {
    display: grid;
    grid-template-columns: 1fr;
    gap: 2vw;
  }
  .image {
    background: #828282;
    height: 700px;
  }
  .modal {
    padding: 0 30px;
  }
}

@media only screen and (min-width: 769px) and (max-width: 1024px) {
  .gallery {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 2vw;
  }
  .image {
    background: #828282;
    height: 700px;
  }
}
</style>
