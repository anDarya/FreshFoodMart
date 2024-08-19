<template>
  <div class="relative flex flex-col lg:flex-row-reverse">
    <div class="background-image w-full lg:w-2/3 bg-cover bg-center height-container lg:relative">
    </div>
    <div class="absolute inset-0 bg-[#cedada]/75 lg:relative lg:bg-[#cedada] lg:w-1/3 bg-cover bg-center height-container grid grid-rows-2 z-10 flex flex-col justify-center lg:items-start lg:pl-14">
      <div class="flex flex-col items-center lg:items-start justify-end w-full h-full text-black-700 text-5xl font-bold space-y-4 lg:text-left">
        <div class="flex justify-center lg:justify-start">Make healthy</div>
        <div class="flex justify-center lg:justify-start">life with 
          <p class="italic text-green-700 underline underline-offset-4 decoration-green-700 ml-2">fresh</p>
        </div>
        <div class="flex justify-center lg:justify-start">grocery</div>
      </div>
      <div class="flex flex-col items-center lg:items-start text-left text-black-500 text-lg space-y-4">
        <div class="px-14 lg:px-0 py-4">Get the best quality and most delicious grocery food in
          the world, you can get them all using our website
        </div>
        <button class="w-40 h-12 mt-4 lg:ml-0">Shop now</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.background-image {
  background-image: url(../assets/images/vegetables.jpg);
  background-size: cover;
  background-position: center;
  box-shadow: inset 0px 0px 35px 35px #cedada;
}
.height-container {
  height: calc(100vh - 78px);
}
</style>