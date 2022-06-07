<template>
   <div class="mt-10 relative w-full px-4 sm:mx-auto sm:max-w-lg">
        <img class="absolute bottom-0 -right-5 sm:-top-5 h-16" src="@/assets/circlemiddle.png" alt="">
            <div v-for="{current, location, } in tempInfo" :key="location.name" class="p-6 rounded-lg backdrop-blur-xl backdrop-filter bg-drop">
            <h2 class="text-white text-2xl font-medium text-center leading-none">{{location.name}}</h2>
                <div class="text-center text-white">
                    <p class="relative mt-10 text-white text-7xl font-medium" >{{current.temp_c}}<sup class="absolute top-0 text-base">0</sup>C</p>
                    <span class="text-lg">{{current.condition.text}}</span>
                </div>
                <div class="mt-10 flex items-center justify-center text-center text-white overflow-x-auto" >
                    <div class="text-center">
                        <span class="font-medium">{{location.localtime}}</span>
                        <div class="flex justify-center">
                        <img class="w-12 h-12" :src="current.condition.icon" alt="weathericon">
                        </div>
                        <!-- <svg class="w-8 h-8" width="30" height="30" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M20.203.938c1.5 2.25 2.39 4.968 2.39 7.875.048 7.828-6.374 14.156-14.296 14.156-2.672 0-5.203-.75-7.36-2.016 2.438 4.828 7.454 8.11 13.266 8.11 8.203 0 14.86-6.563 14.86-14.672 0-6-3.657-11.157-8.86-13.454Z" fill="#FFCE31"/></svg> -->
                        <span class="font-medium">{{current.temp_c}} <sup>0</sup>c</span>
                    </div>
                </div>

                <div class="mt-5 border-t border-[#B7B7B7]" />

                <div class="mt-1 text-white font-medium">
                    <p>Details</p>
                    <div class="flex items-baseline space-x-4">
                        <div>
                            <img src="@/assets/sunrise.png" alt="">
                            <span>06:44</span>
                        </div>
                        <div class="inline-flex">
                            <img class="w-auto" src="@/assets/semi.png" alt="">
                            </div>
                            <div>
                                <img src="@/assets/sunset.png" alt="">
                                <span>17:58</span>
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
export default {
    props:['tempInfo']

}
</script>
