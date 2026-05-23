<script setup>
import { ref, computed, onMounted, onBeforeUnmount } from 'vue'
import { 
  LifeBuoy as SosIcon,
  Hammer as HammerIcon,
  CalendarDays as CalendarIcon,
  Logs as MenuIcon,
  MessagesSquare as ChatIcon
} from '@lucide/vue'
//import { Map } from '@lucide/vue'
//import { PencilRuler } from '@lucide/vue'
//import { CircleUserRound } from '@lucide/vue'
//import { ScanQrCode } from '@lucide/vue'
import Logo from '../../assets/ikona.png'

import { useApiDataStore } from '../../stores/api.js'
import { IonNavLink, IonTabBar } from '@ionic/vue'

// store instance (was previously accessed through mapStores in Options API)
const apiDataStore = useApiDataStore()

// reactive state
const showIosInstallMessage = ref(false)
const versionTimer = ref(null)

// computed helpers
const isIos = computed(() => {
  const userAgent = window.navigator.userAgent.toLowerCase()
  return /iphone|ipod/.test(userAgent)
})

const isInStandaloneMode = computed(() => {
  return ('standalone' in window.navigator) && (window.navigator.standalone)
})

const iOSversion = computed(() => {
  const userAgent = window.navigator.userAgent
  if (/iP(hone|od|ad)/.test(userAgent)) {
    const v = userAgent.match(/OS (\d+)_(\d+)_?(\d+)?/)
    return [parseInt(v[1], 10), parseInt(v[2], 10), parseInt(v[3] || 0, 10)]
  }
  return false
})

onMounted(() => {
  // trigger permissions fetch (previously in mounted())
  apiDataStore.permissions.fetchData()
})

onBeforeUnmount(() => {
  if (versionTimer.value) clearInterval(versionTimer.value)
});
</script>

<template>
  <IonTabBar class="navigation-bar">

    <div class="navigation-bar__content">

      <IonNavLink router-link="/sos" router-direction="none">
        <div class="navigation_bar__item">
          <component :is="SosIcon" aria-label="sos" />
          <p>SOS</p>
        </div>
      </IonNavLink>


      <IonNavLink router-link="/warsztaty" router-direction="none"
        v-if="!apiDataStore.permissions.ready || !apiDataStore.permissions.data.length">
        <div class="navigation_bar__item">
          <component :is="HammerIcon" aria-label="warsztaty" />
          <p>Warsztaty</p>
        </div>
      </IonNavLink>
      <IonNavLink router-link="/admin-menu" router-direction="none" v-else>
        <div class="navigation_bar__item">
          <component :is="MenuIcon" aria-label="menu" />
          <p>Menu</p>
        </div>
      </IonNavLink>


      <IonNavLink router-link="/" router-direction="none">
        <div class="navigation-bar__logo">
          <img :src="Logo" alt="logo" />
        </div>
      </IonNavLink>
      <IonNavLink router-link="/harmonogram" router-direction="none">
        <div class="navigation_bar__item">
          <component :is="CalendarIcon" aria-label="harmonogram" />
          <p>Harmonogram</p>
        </div>
      </IonNavLink>
      <IonNavLink router-link="/czaty" router-direction="none">
        <div class="navigation_bar__item">
          <component :is="ChatIcon" aria-label="user" />
          <p>Czaty</p>
        </div>
      </IonNavLink>
    </div>

  </IonTabBar>
</template>


<style scoped>
.navigation-bar {
  height: var(--nav-height);
  border: 0;
  /* background-color: #1b1b1bbb; */
  background-color: var(--bg-translusent);
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);

  position: fixed;
  bottom: 0;
  width: 100%;
  left: 0;
  right: 0;

  z-index: 5;
}

.navigation-bar__content {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  max-width: 550px;
  margin: 0 auto;
}

.navigation-bar__logo {
  width: 75px;
  height: 75px;
  border-radius: 50%;
  /* background-color: var(--bg-lighter); */
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: 0px -3px 8px rgba(0, 0, 0, 0.25);
  /* margin: -10px auto 0; */
  position: relative;
  z-index: 110;
  transform: translateZ(10px);
}

.navigation-bar__logo img {
  width: 100%;
  height: 100%;
  max-width: none;
}

.navigation_bar__item {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  color: #fff;
  font-size: 9px;
  text-align: center;

  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  /* height: 50px; */
  height: 100%;
}

.navigation_bar__item {
  overflow: hidden;
}

.navigation_bar__item img {
  filter: drop-shadow(0px 100px 0 var(--theme-dark));
  transform: translateY(-100px);
  width: 24px;
  object-fit: contain;
}

.navigation_bar__item.selected img {
  filter: drop-shadow(0px 100px 0 var(--theme-light));
}
</style>
