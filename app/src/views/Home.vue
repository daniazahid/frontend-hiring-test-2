<template>
  <div class="flex flex-col  h-screen max-h-screen">
    <div class=" z-20 flex justify-center relative bg-hero-pattern bg-cover px-4 pt-8 pb-32">

      <div class="w-full max-w-screen-sm ">
        <h1 class="text-white text-center text-3xl pb-4">IP Address Tracker</h1>
        <div class="flex">
          <input v-model="Ipquery" class="flex-1 py-3 px-2 rounded-tl-md rounded-bl-md focus:outline-none" type="text" placeholder="Search for any IP address or domain">
          <i @click="getIpDetails" class="bg-black text-white px-4 rounded-tr-md rounded-br-md flex items-center cursor-pointer fas fa-chevron-right"></i>
        </div>
      </div>
      <InfoIP v-if="IpInfo" v-bind:IpInfo="IpInfo"/>
    </div>
    

    <div id="mapid" class="h-full z-10"></div>
  </div>
</template>

<script>
// @ is an alias to /src
import InfoIP from "../components/InfoIP.vue";
import leaflet from "leaflet";
import {onMounted, ref} from "vue";
import axios from "axios"

export default {
  name: 'Home',
  components: {
    InfoIP,
    
  },
  setup() {
    let mymap;
    const Ipquery= ref("");
    const IpInfo=ref(null);
    onMounted(()=>{
      mymap = leaflet.map('mapid').setView([51.505, -0.09], 13);


      leaflet.tileLayer('https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token=pk.eyJ1IjoiZGFuaWE3ODYiLCJhIjoiY2tyeTRlNXBiMGlhNTJwbWdxOGY3MTU4ZSJ9.vQtXhtOkSGCL6qfR9PgP3Q', {
    attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors, Imagery © <a href="https://www.mapbox.com/">Mapbox</a>',
    maxZoom: 18,
    id: 'mapbox/streets-v11',
    tileSize: 512,
    zoomOffset: -1,
    accessToken: 'pk.eyJ1IjoiZGFuaWE3ODYiLCJhIjoiY2tyeTRlNXBiMGlhNTJwbWdxOGY3MTU4ZSJ9.vQtXhtOkSGCL6qfR9PgP3Q'
 }).addTo(mymap);
    })

    const getIpDetails=async ()=>{
      try{
        const data= await axios.get(`https://geo.ipify.org/api/v1?apiKey=at_HXtydSrmh702ROxzL7lzEijlaEXrb&ipAddress=${Ipquery.value}`);
        const result= data.data;
        console.log(result);
        IpInfo.value={
          address: result.ip,
          state: result.location.region,
          timezone:result.location.timezone,
          isp:result.isp,
          lat:result.location.lat,
          lng:result.location.lng,

        };
        leaflet.marker([IpInfo.value.lat, IpInfo.value.lng]).addTo(mymap);
        mymap.setView([IpInfo.value.lat, IpInfo.value.lng], 13);
      }catch(error){
        // alert(error.message);
      }
    }
    return {Ipquery,IpInfo,getIpDetails};
  },
}
</script>
<style >
body{
font-family: 'Rubik', sans-serif;
font-size: 18px;
color:#333333;
}
</style>