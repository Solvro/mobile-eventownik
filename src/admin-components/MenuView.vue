<script setup>
import TopBar from '../components/navigation/TopBar.vue'
import MenuCard from './MenuCard.vue'

import { 
  LifeBuoy as SosIcon,
  Map as MapIcon,
  Hammer as HammerIcon,
  ScanQrCode as ScannerIcon,
  CirclePlus as PointsIcon,
  Shapes as RankingIcon, // ??
  Megaphone as AnnouncementIcon,
  Bus as BusIcon,
  Users as GroupIcon,
  Boxes as FractionIcon,
  ClipboardPlus as AddPointsIcon
 } from '@lucide/vue'

import { useApiDataStore } from '../stores/api.js'
import { mapStores } from 'pinia'


import { IonPage, IonContent, toastController } from '@ionic/vue'
import { importContacts, deleteContacts } from '@/functions/importContacts'
</script>

<template>
  <ion-page>
    <ion-content :fullscreen="false">
      <main>
        <TopBar title="Menu" />
        <div class="padding cards">
          <MenuCard title="Skaner" :icon="ScannerIcon" link="/skaner" v-if="apiDataStore.permissions.ready &&
            apiDataStore.permissions.hasOneOfPermissions([
              'can_validate_meals',
              'can_view_user_info',
              'can_add_points'
            ])
          " />
          <MenuCard title="Dodaj punkty" :icon="AddPointsIcon" link="/punkty/dodaj" v-if="apiDataStore.permissions.ready &&
            apiDataStore.permissions.hasOneOfPermissions(['can_add_points'])
          " />
          <MenuCard title="Punkty" :icon="PointsIcon" link="/punkty" v-if="apiDataStore.permissions.ready &&
            apiDataStore.permissions.hasOneOfPermissions(['can_view_points'])
          " />
          <MenuCard title="Ranking" :icon="RankingIcon" link="/ranking" v-if="apiDataStore.permissions.ready &&
            apiDataStore.permissions.hasOneOfPermissions(['can_view_points'])
          " />
          <MenuCard title="Frakcje" :icon="FractionIcon" link="/frakcje" />
          <MenuCard title="Gra nocna" :icon="GroupIcon" link="/grupy" v-if="apiDataStore.permissions.ready &&
            apiDataStore.permissions.hasOneOfPermissions(['can_view_groups'])
          " />
          <MenuCard title="Ogłoszenia" :icon="AnnouncementIcon" link="/ogloszenia" v-if="apiDataStore.permissions.ready &&
            apiDataStore.permissions.hasOneOfPermissions(['can_add_announcement'])
          " />
          <MenuCard title="Busy" :icon="BusIcon" link="/busy" v-if="apiDataStore.permissions.ready &&
            apiDataStore.permissions.hasOneOfPermissions(['can_check_bus_presence'])
          " />
          <MenuCard title="Importuj kontakty" :icon="GroupIcon" @click="importContacts" v-if="apiDataStore.permissions.ready &&
            apiDataStore.permissions.hasOneOfPermissions(['can_get_contacts'])
          " />
          <MenuCard title="Usuń kontakty" :icon="GroupIcon" @click="deleteContacts" v-if="apiDataStore.permissions.ready &&
            apiDataStore.permissions.hasOneOfPermissions(['can_get_contacts'])
          " />
          <MenuCard title="Uczestnicy" :icon="GroupIcon" link="/uczestnicy" v-if="apiDataStore.permissions.ready &&
            apiDataStore.permissions.hasOneOfPermissions(['can_change_bands'])
          " />

          <MenuCard title="Warsztaty" :icon="HammerIcon" link="/warsztaty" />
          <MenuCard title="Sos" :icon="SosIcon" link="/sos" />
          <MenuCard title="Mapka" :icon="MapIcon" link="/mapa" />


          <div style="height: calc(33vw - 25px); width: calc(33vw - 25px)"></div>
          <div style="height: calc(33vw - 25px); width: calc(33vw - 25px)"></div>
        </div>
      </main>
    </ion-content>
  </ion-page>
</template>

<style scoped>
.cards {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  margin-top: 20px;
  gap: 12px;
}
</style>

<script>
export default {
  data() {
    return {
    }
  },
  computed: {
    ...mapStores(useApiDataStore)
  },
  methods: {
  }
}
</script>
