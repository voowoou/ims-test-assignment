<template>
  <div class="img-stats-container">
    <div class="stat-container">
      <LikeIcon />
      <div>{{ likes }}</div>
    </div>
    <div class="stat-container">
      <EyeIcon />
      <div>{{ views }}</div>
    </div>
  </div>
</template>

<script>
import LikeIcon from '../icons/LikeIcon.vue';
import EyeIcon from '../icons/EyeIcon.vue';
export default {
  components: { LikeIcon, EyeIcon },
  name: 'ImageStats',
  props: {
    likes: Number,
    views: Number,
  },
};
</script>

<style>
.img-stats-container {
  display: flex;
  width: 100%;
  justify-content: space-around;
  padding: 5px 0;
  color: #828282;
}

.stat-container {
  display: flex;
}

.stat-container div {
  margin-left: 5px;
}
</style>
