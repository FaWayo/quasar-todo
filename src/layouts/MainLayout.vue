<template>
  <q-layout view="lHh Lpr lFf">
    <q-header>
      <q-toolbar>
        <q-btn
          @click="leftDrawerOpen = !leftDrawerOpen"
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
        
        />

      
      </q-toolbar>
       <div class = "q-px-lg q-pt-xl q-mb-md">
         <div class = "text-h3"> Todo App</div>
         <div class = "text-sub1"> {{todaysDate}}</div>
       </div>

       <q-img
       src = "../statics/sunset.jpg"
       class = "header-image absolute-top"/>
      
    </q-header>

    <q-drawer
        v-model="leftDrawerOpen"
        show-if-above
        :width="250"
        :breakpoint="600"
      >
        <q-scroll-area style="height: calc(100% - 150px); margin-top: 185px; border-right: 1px solid #ddd">
          <q-list padding>
            <q-item
            exact
             to = "/"
             clickable v-ripple>
              <q-item-section avatar>
                <q-icon name="list" />
              </q-item-section>

              <q-item-section>
                Todo
              </q-item-section>
            </q-item>

            <q-item 
            exact
            to = "/help"
            clickable v-ripple>
              <q-item-section avatar>
                <q-icon name="help" />
              </q-item-section>

              <q-item-section>
                Help
              </q-item-section>
            </q-item>

            

          </q-list>
        </q-scroll-area>

        <q-img class="absolute-top" src="../statics/sunset.jpg" style="height: 185px">
          <div class="absolute-bottom bg-transparent">
            <q-avatar size="56px" class="q-mb-sm">
              <img src="../statics/avatar.png">
            </q-avatar>
            <div class="text-weight-bold">Fatima Wayo</div>
            <div>@fawayo</div>
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
import { date } from 'quasar'

export default {
  name: 'myLayout',
 
  data(){
    return {
      leftDrawerOpen: false
    }
  },
  computed: {
    todaysDate () {
      const timeStamp = Date.now()
      return date.formatDate(timeStamp, 'dddd, Do MMMM YYYY. (HH:mm)')
    }
  }
}
</script>


<style lang="scss">
   .header-image {
     height: 100%;
     z-index: -1;
    //  opacity: 0.8;
    //  filter: grayscale(10%)
   }
</style>
