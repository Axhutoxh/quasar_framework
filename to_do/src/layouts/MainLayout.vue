<template>
  <q-layout view="lHh Lpr lFf">
    <q-header >
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="leftDrawerOpen = !leftDrawerOpen"
        />
      </q-toolbar>

      <div class="q-px-lg q-pt-xl q-mb-md">
        <div class="text-h3">Todo</div>
        <div class="text-subtitle">{{todaysDate}}</div>
      </div>

      <q-img 
        src="../img/mountain.jpg"
        class="header-img absolute-top"

      />
    </q-header>

<q-drawer
        v-model="leftDrawerOpen"
        show-if-above
        :width="250"
        :breakpoint="600"
      >
        <q-scroll-area style="height: calc(100% - 185px); margin-top: 185px; border-right: 1px solid #ddd">
          <q-list padding>
            <q-item 
               to="/"
               exact
               clickable 
               v-ripple>
              <q-item-section avatar>
                <q-icon name="list" />
              </q-item-section>

              <q-item-section>
                Todo
              </q-item-section>
            </q-item>

            <q-item
              to='/help'
              exact
              clickable
              v-ripple>
              <q-item-section avatar>
                <q-icon name="help" />
              </q-item-section>

              <q-item-section>
                Help
              </q-item-section>
            </q-item>

          </q-list>
        </q-scroll-area>

        <q-img class="absolute-top" src="../img/mountain.jpg" style="height: 185px">
          <div class="absolute-bottom bg-transparent">
            <q-avatar size="56px" class="q-mb-sm">
              <img src="../img/pic.png">
            </q-avatar>
            <div class="text-weight-bold">Ashutosh Chandra</div>
            <div>@Axhutoxh</div>
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

export default {
  name: 'MainLayout',
  data () {
    return {
      leftDrawerOpen: false,
   }
  },
  computed: {
    todaysDate () {
      let timeStamp = Date.now()
      return(date.formatDate(timeStamp, 'dddd D MMMM'))

    }
  },  
}
</script>
<style lang="scss">
  .header-img{
    height: 100%;
    z-index: -1;
    opacity: 0.4;
    filter: grayscale(10%);
  }
</style>