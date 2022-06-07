<template>
  <div class="relative bg-black flex min-h-screen flex-col justify-center">
      <img class="absolute top-0 w-auto" src="@/assets/circletop.png" alt="BIGBLUECIRCLE">
      <div class="absolute left-[57%] bottom-0">
        <img class="w-auto" src="@/assets/circlebottom.png" alt="CIRCLE">
      </div>

      <!-- error notification --> 
        <div aria-live="assertive" class="fixed inset-0 flex items-end px-4 py-6 pointer-events-none sm:p-6 sm:items-start">
          <div class="w-full flex flex-col items-center space-y-4 sm:items-end">
            <!-- Notification panel, dynamically insert this into the live region when it needs to be displayed -->
            <transition enter-active-class="transform ease-out duration-300 transition" enter-from-class="translate-y-2 opacity-0 sm:translate-y-0 sm:translate-x-2" enter-to-class="translate-y-0 opacity-100 sm:translate-x-0" leave-active-class="transition ease-in duration-100" leave-from-class="opacity-100" leave-to-class="opacity-0">
              <div v-if="show" class="max-w-sm w-full bg-rose-50 shadow-lg rounded-lg pointer-events-auto ring-1 ring-black ring-opacity-5 overflow-hidden">
                <div class="p-4">
                  <div class="flex items-start">
                    <div class="flex-shrink-0">
                      <ShieldExclamationIcon class="h-6 w-6 text-rose-600" aria-hidden="true" />
                    </div>
                    <div v-for="err in error" :key="err" class="ml-3 w-0 flex-1 pt-0.5">
                      <p class="text-sm font-medium text-rose-600 capitalize">{{err}} </p>
                    </div>
                    <div class="ml-4 flex-shrink-0 flex">
                      <button type="button" @click="show = false" class="bg-white rounded-md inline-flex text-gray-400 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                        <span class="sr-only">Close</span>
                        <XIcon class="h-5 w-5" aria-hidden="true" />
                      </button>
                    </div>
                  </div>
                </div>
              </div>
            </transition>
          </div>
        </div>
      <!-- end error -->

      <div class="mt-1 relative flex items-center w-full mx-auto max-w-lg px-4 sm:px-0">
          <input type="text" name="search" id="search" v-model="query" @keyup.enter.prevent="weatherQuery" class="backdrop-blur-xl backdrop-filter bg-drop shadow-sm focus:ring-sky-500 focus:border-sky-500 block  w-full pr-12 sm:text-base border-transparent rounded-md text-gray-200 placeholder:text-gray-200" placeholder="Search for city..."/>
          <div class="absolute inset-y-0 left-0 flex py-1.5 pr-1.5">
          </div>
      </div>     

      <transition enter-active-class="transform ease-out duration-300 transition" enter-from-class="translate-y-2 opacity-0 sm:translate-y-0 sm:translate-x-2" enter-to-class="translate-y-0 opacity-100 sm:translate-x-0" leave-active-class="transition ease-in duration-100" leave-from-class="opacity-100" leave-to-class="opacity-0">
       <!-- component -->
       <weather-info :tempInfo="tempInfo"></weather-info>
      </transition>
  </div>
</template>

<script>
import {ref} from 'vue'
import { ShieldExclamationIcon } from '@heroicons/vue/outline'
import { XIcon } from '@heroicons/vue/solid'
import WeatherInfo from '@/components/WeatherInfo.vue'

export default {
  name: 'HomeView',
  components:{ShieldExclamationIcon,XIcon,WeatherInfo},
  
  setup() {
    const tempInfo = ref([])
    const error = ref([])
    const query = ref('')
    const show = ref(false)
    return {
      tempInfo,
      error,
      show,
      query,
      url: process.env.VUE_APP_API_URL,
      secret: process.env.VUE_APP_API_KEY,
    }
  },
  methods:{
    async weatherQuery() {
      if (this.query !== '') {
      await fetch(`${this.url}?key=${this.secret}&q=${this.query}`,
      { method: "GET"})
      .then(response => response.json())
      .then(data => {
          this.tempInfo = []
          this.tempInfo.push(data)

          if(data.error.code == 1006) {
              this.show = true;
              this.error = [];
              this.error.push(data.error.message)

              setTimeout(() => {
              this.show = false
              this.query = ''
            }, 4000);
          } 
      }).catch(e => {
        if (e instanceof TypeError) {
          throw new Error(e);
        }
      })
    }
    }
  }
}
</script>
