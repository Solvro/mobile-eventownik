<script setup>
import ItemBox from '../components/ItemBox.vue'
import TopBar from '../components/navigation/TopBar.vue'
import LoadingIndicator from '../components/LoadingIndicator.vue'

import { 
  Utensils as mealIcon,
  CircleUserRound as userIcon,
  CirclePlus as pointsIcon,
  ChevronRight as arrow
} from '@lucide/vue'

import { useApiDataStore } from '../stores/api.js'
import { mapStores } from 'pinia'
import { IonPage, IonContent } from '@ionic/vue';
</script>

<template>
  <ion-page>
    <ion-content :fullscreen="false">
      <main>
        <TopBar title="Skaner" />
        <div class="padding-main">
          <RouterLink to="/skaner/posilki" v-if="
            apiDataStore.permissions.ready &&
            apiDataStore.permissions.hasPermission('can_validate_meals')
          ">
            <ItemBox bigText="Walidacja posiłków" :leftIcon="mealIcon" :rightIcon="arrow" noRoundIcon leftIconWhite />
          </RouterLink>

          <RouterLink to="/skaner/punkty" v-if="
            apiDataStore.permissions.ready && apiDataStore.permissions.hasPermission('can_add_points')
          ">
            <ItemBox bigText="Dodaj punkty" :leftIcon="pointsIcon" :rightIcon="arrow" noRoundIcon leftIconWhite />
          </RouterLink>

          <RouterLink to="/skaner/uczestnik" v-if="
            apiDataStore.permissions.ready &&
            apiDataStore.permissions.hasPermission('can_view_user_info')
          ">
            <ItemBox bigText="Informacje o uczestniku" :leftIcon="userIcon" :rightIcon="arrow" noRoundIcon
              leftIconWhite />
          </RouterLink>
        </div>
        <LoadingIndicator v-if="!apiDataStore.permissions.ready" />
      </main>
    </ion-content>
  </ion-page>
</template>

<script>
export default {
  computed: {
    ...mapStores(useApiDataStore)
  },
  mounted() { }
}
</script>
