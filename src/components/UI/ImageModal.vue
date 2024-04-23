<template>
  <div class="modal">
    <div class="modal-content" @click="$emit('close')">
      <span class="close" @click="$emit('close')">&times;</span>
      <img :src="src" :alt="alt" />
      <ImageStats :likes="likes" :views="views" class="image-stats" />
    </div>
  </div>
</template>

<script>
import ImageStats from './ImageStats.vue';

export default {
  components: { ImageStats },
  name: 'ImageModal',
  props: {
    src: String,
    alt: String,
    likes: Number,
    views: Number,
  },
  emits: ['close'],
};
</script>

<style>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.75);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 10;
}
.modal-content {
  position: relative;
  padding: 10px;
  background: white;
  border-radius: 10px;
}
.close {
  position: absolute;
  top: -10px;
  right: -30px;
  font-size: 30px;
  cursor: pointer;
  color: white;
}

.image-stats {
  margin-top: 10px;
}
</style>
