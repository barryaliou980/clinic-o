<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          @click="toggleLeftDrawer"
          icon="menu"
          aria-label="Menu"
        />
        <q-toolbar-title>
          Quasar App
        </q-toolbar-title>
        <q-space/>
        <div class="q-gutter-sm row items-center no-wrap">       
          <q-btn round flat>
            <q-avatar size="26px">
              <img src="https://cdn.quasar.dev/img/boy-avatar.png">
            </q-avatar>
              <q-menu>
          <q-list style="min-width: 100px">
            <q-item clickable @click="logOut">
              <q-item-section>Deconnection</q-item-section>
            </q-item>
              <q-separator />
            <q-item clickable v-close-popup>
              <q-item-section>Parameters</q-item-section>
            </q-item>
            <q-separator />
          </q-list>
        </q-menu>
          </q-btn>
        </div>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      class="bg-primary text-white"
    >
      <q-list>
        <q-item to="/" active-class="q-item-no-link-highlighting">
          <q-item-section avatar>
            <q-icon name="dashboard"/>
          </q-item-section>
          <q-item-section>
            <q-item-label>Dashboard</q-item-label>
          </q-item-section>
        </q-item>

        <q-item to="/add-patient" active-class="q-item-no-link-highlighting">
          <q-item-section avatar>
            <q-icon name="note_add"/>
          </q-item-section>
          <q-item-section>
            <q-item-label>Add New Patient</q-item-label>
          </q-item-section>
        </q-item>

        <q-item to="/list-patients" active-class="q-item-no-link-highlighting">
          <q-item-section avatar>
            <q-icon name="people"/>
          </q-item-section>
          <q-item-section>
            <q-item-label>List Patients</q-item-label>
          </q-item-section>
        </q-item>

         <q-item  v-if="store.loggedUser.user_type==='admin'" to="/users" active-class="q-item-no-link-highlighting">
          <q-item-section avatar>
            <q-icon name="people"/>
          </q-item-section>
          <q-item-section>
            <q-item-label>Utilisateurs</q-item-label>
          </q-item-section>
        </q-item>


        <q-expansion-item
          icon="trending_up"
          label="Statistics"
        >
          <q-list class="q-pl-lg">
            <q-item to="/MapMarker" active-class="q-item-no-link-highlighting">
              <q-item-section avatar>
                <q-icon name="people"/>
              </q-item-section>
              <q-item-section>
                <q-item-label>Patient</q-item-label>
              </q-item-section>
            </q-item>
            <q-item to="/analytics" active-class="q-item-no-link-highlighting">
              <q-item-section avatar>
                <q-icon name="streetview"/>
              </q-item-section>
              <q-item-section>
                <q-item-label>RDT TEST</q-item-label>
              </q-item-section>
            </q-item>
          </q-list>
        </q-expansion-item>

      </q-list>
    </q-drawer>

    <q-page-container class="bg-grey-2">
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
// import EssentialLink from '../components/EssentialLink.vue'
// import Messages from './Messages.vue';
// import {useQuasar} from 'quasar';

import { defineComponent, ref } from 'vue'
import { useUserStore } from '../stores/userStore';

export default defineComponent({
  name: 'MainLayout',

  components: {
    // Messages
  },
  methods:{
    async logOut(){
     await this.store.logout()
     window.location.reload()

    }
  },

  setup () {
    const leftDrawerOpen = ref(false)
    //  const $q = useQuasar()

    return {
      store: useUserStore(),
      leftDrawerOpen,
      toggleLeftDrawer () {
        leftDrawerOpen.value = !leftDrawerOpen.value
      }
    }
  }
})
</script>
