<template>
  <q-layout view="lHh Lpr lFf">
    <!-- header -->
    <q-header>

      <!-- toggle btn -->
      <q-toolbar>
        <q-btn flat dense round icon="menu" aria-label="Menu" @click="toggleLeftDrawer" />


      </q-toolbar>

      <!-- nav text -->
      <div class="q-px-lg q-pt-xl q-mb-md">
        <!-- header -->
        <div class="text-h3">
          Todo
        </div>
        <!-- sub heading -->
        <div class="text-subtitle">
          {{ todaysDate }}
        </div>
      </div>

      <q-img src="https://i.postimg.cc/HLvn3rwp/mountains-1412683-1280.png" alt="" class="header-image absolute-top" />
    </q-header>

    <!-- SIDENAV -->
    <q-drawer v-model="leftDrawerOpen" show-if-above :width="250" :breakpoint="600">
      <q-scroll-area style="height: calc(100% - 185px); margin-top: 185px; border-right: 1px solid #ddd">
        <q-list padding>

          <q-item to="/" exact clickable v-ripple>
            <q-item-section avatar>
              <q-icon name="list" />
            </q-item-section>

            <q-item-section>
              Todo
            </q-item-section>
          </q-item>

          <q-item to="help" exact clickable v-ripple>
            <q-item-section avatar>
              <q-icon name="help" />
            </q-item-section>

            <q-item-section>
              Help
            </q-item-section>
          </q-item>



        </q-list>
      </q-scroll-area>

      <q-img class="absolute-top" src="https://i.postimg.cc/HLvn3rwp/mountains-1412683-1280.png" style="height: 185px">
        <div class="absolute-bottom bg-transparent">
          <q-avatar size="56px" class="q-mb-sm">
            <img src="https://i.postimg.cc/Bnb764GL/18b9ffb2a8a791d50213a9d595c4dd52.jpg">
          </q-avatar>
          <div class="text-weight-bold">Shane Stevens</div>
          <div>@BEASTxk9</div>
        </div>
      </q-img>
    </q-drawer>

    <q-page-container>

      <keep-alive>
        <router-view />
      </keep-alive>

    </q-page-container>
  </q-layout>
</template>

<script>
import { date } from 'quasar';
import { defineComponent, ref } from 'vue'
import EssentialLink from 'components/EssentialLink.vue'

const linksList = [
  {
    title: 'Docs',
    caption: 'quasar.dev',
    icon: 'school',
    link: 'https://quasar.dev'
  },
  {
    title: 'Github',
    caption: 'github.com/quasarframework',
    icon: 'code',
    link: 'https://github.com/quasarframework'
  },
  {
    title: 'Discord Chat Channel',
    caption: 'chat.quasar.dev',
    icon: 'chat',
    link: 'https://chat.quasar.dev'
  },
  {
    title: 'Forum',
    caption: 'forum.quasar.dev',
    icon: 'record_voice_over',
    link: 'https://forum.quasar.dev'
  },
  {
    title: 'Twitter',
    caption: '@quasarframework',
    icon: 'rss_feed',
    link: 'https://twitter.quasar.dev'
  },
  {
    title: 'Facebook',
    caption: '@QuasarFramework',
    icon: 'public',
    link: 'https://facebook.quasar.dev'
  },
  {
    title: 'Quasar Awesome',
    caption: 'Community Quasar projects',
    icon: 'favorite',
    link: 'https://awesome.quasar.dev'
  }
]

export default defineComponent({
  name: 'MainLayout',

  components: {
    EssentialLink
  },

  setup() {
    const leftDrawerOpen = ref(false)

    return {
      essentialLinks: linksList,
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value
      }
    }
  },

  computed: {
    todaysDate() {
      const timeStamp = Date.now()
      return date.formatDate(timeStamp, 'dddd D MMMM YYYY')
    }
  }
})
</script>

<style lang="scss">
.header-image {
  height: 100%;
  z-index: -1;
  opacity: 0.2;
  filter: grayscale(100%);
}
</style>
