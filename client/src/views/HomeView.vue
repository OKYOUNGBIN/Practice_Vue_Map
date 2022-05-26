<template>
  <div class="h-screen relative">
    <div id="map" class="h-full z-[1]"></div>
  </div>
</template>

<script>
import leaflet from "leaflet";
import { onMounted, ref } from "vue";

export default {
  name: "HomeView",
  components: {},
  setup() {
    let map;
    onMounted(() => {
      // init map
      map = leaflet.map("map").setView([28.538336, -81.379234], 10);

      // add tile layer
      leaflet
        .tileLayer(
          `https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token=${process.env.VUE_APP_API_KEY}`,
          {
            attribution:
              'Map data &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors, Imagery © <a href="https://www.mapbox.com/">Mapbox</a>',
            maxZoom: 18,
            id: "mapbox/streets-v11",
            tileSize: 512,
            zoomOffset: -1,
            accessToken: process.env.VUE_APP_API_KEY,
          }
        )
        .addTo(map);

      getGeolocation();
    });

    const coords = ref(null);
    const fechCoords = ref(null);
    const geoMarker = ref(null);

    const getGeolocation = () => {
      fechCoords.value = true;
      navigator.geolocation.getCurrentPosition(setCoords, getLocError);
    };

    const setCoords = (pos) => {
      // stop fetching coords
      fechCoords.value = null;

      // set coords in session storage
      const setSessionCoords = {
        lat: pos.coords.latitude,
        lng: pos.coords.longitude,
      };

      // 설정
      sessionStorage.setItem("coords", JSON.stringify(setSessionCoords));

      // set ref coords value
      coords.value = setSessionCoords;

      plotGeolocation(coords);
    };

    const getLocError = (err) => {
      console.log(err);
    };

    return { coords, geoMarker };
  },
};
</script>
