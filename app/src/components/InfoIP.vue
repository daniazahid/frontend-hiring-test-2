<template>
  <div class="absolute -bottom-64 lg:-bottom-20 flex flex-col lg:flex-row bg-white gap-y-4 gap-x-12 px-8 pt-8 pb-12 rounded-md">
      <div class="flex flex-col ">
          <h3 class="text-xs mb-4 uppercase">IP Address</h3>
          <span class="text-2xl">{{IpInfo.address}}</span>
      </div>

      <div class="flex flex-col ">
          <h3 class="text-xs mb-4 uppercase">Location</h3>
          <span class="text-2xl">{{IpInfo.state}}</span>
      </div>

      <div class="flex flex-col ">
          <h3 class="text-xs mb-4 uppercase">TimeZone</h3>
          <span class="text-2xl">{{IpInfo.timezone}}</span>
      </div>

      <div class="flex flex-col ">
          <h3 class="text-xs mb-4 uppercase">ISP</h3>
          <span class="text-2xl">{{IpInfo.isp}}</span>
      </div>
  </div>
</template>

<script>
export default {
    props:["IpInfo"],
}
</script>
<style>
.v-divider{
  margin-left:5px; 
  margin-right:5px;
 width:1px;
 height:100%;
 border-left:1px solid gray;
 }
</style>