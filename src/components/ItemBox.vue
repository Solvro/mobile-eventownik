<script setup>
defineProps({
  bigText: {
    type: String,
    required: true
  },
  smallText: {
    type: String,
    required: false
  },
  leftBigText: {
    type: String,
    required: false
  },
  bgColor: {
    type: String,
    required: false,
    default: 'var(--primary)'
  },
  leftIcon: {
    type: [Object, String, Function],
    required: false
  },
  leftIconWhite: {
    type: Boolean,
    required: false,
    default: false
  },
  noRoundIcon: {
    type: Boolean,
    required: false,
    default: false
  },
  rightIcon: {
    type: [Object, String, Function],
    required: false
  },
  small: {
    type: Boolean,
    required: false,
    default: false
  }
});
</script>

<template>
  <div class="item" :style="{ backgroundColor: bgColor }" :class="{ small: small }">
    <div class="item-left">
      <img v-if="leftIcon && typeof leftIcon === 'string'" :src="leftIcon" :class="['left-icon', { 'white-icon': leftIconWhite }]" />
      <component v-else-if="leftIcon" :is="leftIcon" :class="['left-icon', { 'white-icon': leftIconWhite }]" />
      <h6 v-if="leftBigText">{{ leftBigText }}</h6>
      <div class="text">
        <h5>{{ bigText }}</h5>
        <p v-if="smallText">{{ smallText }}</p>
      </div>
    </div>
    <img v-if="rightIcon && typeof rightIcon === 'string'" :src="rightIcon" class="right-icon"/>
    <component v-else-if="rightIcon" :is="rightIcon" class="right-icon"/>
    <slot></slot>
  </div>
</template>

<style scoped>
.item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-direction: row;
  padding: 10px 12px;
  border-radius: var(--radius);
  margin: 15px 0;

  min-height: 60px;

  backdrop-filter: blur(10px) !important;
  -webkit-backdrop-filter: blur(10px) !important;
  cursor: pointer;
}

.item-left {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  flex-direction: row;
  gap: 12px;
}

h5 {
  margin: 0;
  padding: 1px;
  font-size: 17px;
  line-height: 19px !important;
  color: var(--primary-foreground);
}

h6 {
  margin: 0;
  padding: 1px;
  font-size: 12px;
  line-height: 13px !important;
  color: var(--primary-foreground);
}


p {
  margin: 0;
  padding: 1px;
  font-size: 11px;
  line-height: 11px !important;
  color: var(--primary-foreground);
}

.white-icon {
  filter: brightness(0) invert(1);
  color: white;
}

.right-icon {
  max-height: 25px;
  max-width: 25px;
  height: 25px;
  width: 25px;
  display: flex;
  margin-left: 10px;
}

.left-icon {
  width: 40px;
  height: 30px;
  object-fit: cover;
}
img.left-icon {
  height: 40px;
  width: 40px;
  object-fit: contain;
}

.small .left-icon {
  margin-left: 0;
  width: 28px;
  height: 28px;
}

.small {
  min-height: 45px;
  padding: 5px 15px;
}
</style>
