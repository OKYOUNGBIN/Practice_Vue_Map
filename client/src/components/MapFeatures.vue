<template>
  <div
    class="w-fu;; md:w-auto absolute md:top-[40px] md:left-[60px] z-[2] flex gap-4 px-6 py-8 md:px-0 md:py-0 bg-transparent"
  >
    <!-- search -->
    <div class="relative flex-1 md:min-w-[350px]">
      <input
        class="pl-9 pr-4 py-3 text-sm focus:outline-none w-full shadow-md rounded-md"
        type="text"
        placeholder="Start Your Search"
      />
      <!-- search Icon -->
      <div class="absolute top-0 left-[8px] h-full flex items-center"></div>
    </div>
    <!-- Geolocation -->
    <div
      class="px-4 bg-white flex items-center shadow-md rounded-md min-h-[45px]"
      :class="{ 'bg-slate-600': coords }"
      @click="$emit('getGeolocation')"
    >
      <i
        class="fas fa-location-arrow text-state-600 text-[18px]"
        :class="{ 'text-white': coords, 'animate-pulse': fetchCoords }"
      ></i>
    </div>
  </div>
</template>

<script>
export default {
  props: ["coords", "fetchCoords"],
};
</script>
