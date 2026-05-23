<script setup>
import { 
  BottleWine as alcohol1,
  Martini as alcohol2,
  Wine as alcohol3,
  Beer as alcohol4,
  GlassWater as alcohol5
} from "@lucide/vue";

defineProps({
  inline: {
    type: Boolean,
    default: false
  },
  small: {
    type: Boolean,
    default: false
  }
});
</script>

<template>
  <div :class="{ loading_indicator: !inline }">
    <div class="spinner_and_img">
      <div
        class="loading_indicator__spinner"
        :class="{ loading_indicator__spinner_small: small }"
      ></div>
      <component v-if="alcoholSrc && !small" class="alcohol" :is="alcoholSrc" aria-label="alcohol"/>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      alcoholSrc: ""
    }
  },
  mounted() {
    const alcohols = [
      alcohol1,
      alcohol2,
      alcohol3,
      alcohol4,
      alcohol5
    ];
    const random = Math.floor(Math.random() * alcohols.length);
    this.alcoholSrc = alcohols[random];
  },
  
}
</script>

<style scoped>

.spinner_and_img {
  position: relative;
  display: grid;
  place-items: center;
  z-index: 300;
}
.alcohol {
  width: 36px;
  height: 36px;
  position: absolute;
  top: calc(50% - 18px);
  left: calc(50% - 18px);
  opacity: 0.5;
}

.loading_indicator {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: grid;
  place-items: center;
}

.loading_indicator__spinner {
  width: 70px;
  height: 70px;
  border-radius: 50%;
  border: 5px solid var(--text-gray);
  border-top-color: var(--text);
  animation: spin 0.5s linear infinite;

}

.loading_indicator__spinner_small {
  width: 16px;
  height: 16px;
  border: 2px solid var(--text-gray);
  border-top-color: var(--text);
}

@keyframes spin {
  to {
    transform: rotate(360deg);
  }
}
</style>
