<template>
  <svg
    width="150px"
    height="200px"
    xmlns="http://www.w3.org/2000/svg"
    xmlns:xlink="http://www.w3.org/1999/xlink"
  >
    <path
      fill="none"
      stroke="#FFF"
      stroke-width="3"
      stroke-linecap="round"
      stroke-linejoin="round"
      stroke-miterlimit="10"
      d="M73 195.4c15.8 0 22.2-5.9 22.2-5.9v-4.6H120v-43.4L102.5 127v30.5s-7.2-2.1-7.1-9.6c.1-6 
    .1-12 0-18-.1-7.1.2-14.1-.2-21.2-1.1-18.6-4.2-37.5-12.9-54.1-2.5-4.8-9.5-16.6-15.6-8.7-4.1 5.3-6.6 11.8-9 18-2.6 6.9-4.7 
    14-6.3 21.1l-.3 1.5c-4.3 19.8-3 39.2-3 39.2l-24.2 23.5v26.1l23.9 3.2v19.8H53l12.2-9.5v-48.1l-4.1-1.4-9.9 23.7"
    />
  </svg>
</template>

<style scoped>
  svg {
  animation: draw 2s linear alternate infinite;
  animation-delay: 1s;
  stroke-dasharray: 580;
  stroke-dashoffset: -580;
}

@keyframes draw {
  to { 
    stroke-dashoffset: 0;
  }
}

</style>