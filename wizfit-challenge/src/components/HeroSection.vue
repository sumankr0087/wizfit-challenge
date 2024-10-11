<template>
  <div class="flex-container">
    <p class="title">What is WizFit Challenge?</p>
    <button class="watch-button">
      <svg style="height: 25px;" viewBox="0 0 20 20" fill="currentColor" class="size-5 icon">
        <path
          d="M6.3 2.84A1.5 1.5 0 0 0 4 4.11v11.78a1.5 1.5 0 0 0 2.3 1.27l9.344-5.891a1.5 1.5 0 0 0 0-2.538L6.3 2.841Z" />
      </svg>
      Watch Video
    </button>
  </div>
  <img :src="playerImage" alt="Banner" class="player-image" />
</template>
  
<script>
export default {
  data() {
    return {
      playerImage: require('@/assets/player.png'),
    };
  },
};
</script>
  
<style scoped>
.flex-container {
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
}

.title {
  color: rgb(208, 4, 4);
  font-size: 24px;
  font-weight: 600;
}

.watch-button {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 8px;
  width: 8rem;
  background-color: rgb(208, 4, 4);
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 14px;
  font-weight: 700;
  margin-left: 25px;
}

.icon {
  margin-right: 5px;
}

.player-image {
  display: block;
  margin: 20px auto auto;
  height: 24rem;
}
</style>
  