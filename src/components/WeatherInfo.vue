<template>
   <div class="mt-10 relative w-full px-4 sm:mx-auto sm:max-w-lg">
        <img class="absolute bottom-0 -right-5 sm:-top-5 h-16" src="@/assets/circlemiddle.png" alt="">
            <div v-for="{current, location,forecast } in tempInfo" :key="location.name" class="p-6 rounded-lg backdrop-blur-xl backdrop-filter bg-drop">
            <h2 class="text-white text-2xl font-medium text-center leading-none">{{location.name}}</h2>
                <div class="text-center text-white">
                    <p class="relative mt-10 text-white text-7xl font-medium" >{{current.temp_c}}<sup class="absolute top-0 text-base">0</sup>C</p>
                    <span class="text-lg">{{current.condition.text}}</span>
                </div>
                <div v-for="cast in forecast.forecastday" :key="cast.date"  class="mt-10 pl-3 flex items-center justify-center gap-x-4 text-center text-white scrollbar overflow-x-auto" >
                    <div v-for="hr in cast.hour" :key="hr.time" class="px-2 text-center">
                        <span class="font-medium">{{moment(hr.time).format('HH:mm')}}</span>
                        <div class="flex justify-center">
                            <img class="w-auto h-10" :src="hr.condition.icon" alt="weathericon">
                        </div>
                        <span class="text-xs whitespace-nowrap">{{hr.temp_c}} <sup>0</sup>c</span>
                    </div>
                </div>

                <div class="mt-5 border-t border-[#B7B7B7]" />

                <div class="mt-1 text-white font-medium lowercase">
                    <p>Details</p>
                    <div v-for="cast in forecast.forecastday" :key="cast.date" class="flex items-baseline space-x-4">
                        <div>
                            <img class="w-16 h-auto" src="@/assets/sunrise.png" alt="">
                            <span class="text-xs">{{cast.astro.sunrise}}</span>
                        </div>
                        <div class="inline-flex">
                            <img class="w-auto" src="@/assets/semi.png" alt="">
                            </div>
                            <div>
                                <img class="w-16 h-auto" src="@/assets/sunset.png" alt="">
                                <span class="text-xs">{{cast.astro.sunset}}</span>
                            </div>
                        </div>
                </div>

                <div class="mt-8 max-w-sm mx-auto flex items-center justify-between">
                    <div class="inline-block text-center">
                        <p class="font-medium text-white text-lg">{{current.feelslike_c}} <sup>0</sup>c</p>
                        <span class="text-sm text-[#B7B7B7]">RealFeel</span>
                    </div>
                    <div class="inline-block text-center">
                        <p class="font-medium text-white text-lg">{{current.humidity}}%</p>
                        <span class="text-sm text-[#B7B7B7]">Humidity</span>
                    </div>
                    <div class="inline-block text-center">
                        <p class="font-medium text-white text-lg">{{current.wind_kph}}3</p>
                        <span class="text-sm text-[#B7B7B7]">W,force</span>
                    </div>
                    <div class="inline-block text-center">
                        <p class="font-medium text-white text-lg">{{current.pressure_mb}}hPa</p>
                        <span class="text-sm text-[#B7B7B7]">Pressure</span>
                    </div>
                </div>

            </div>
    </div>
</template>

<script>
import moment from 'moment'
export default {
    props:['tempInfo'],

    setup() {
        return {
            moment
        }
    }

}
</script>