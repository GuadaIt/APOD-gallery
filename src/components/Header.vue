<template>
  <header>
      <a href="https://apod.nasa.gov/apod/astropix.html" target="_blank" rel="noopener noreferrer">
      </a>
      <p>Astronomy Picture of the Day</p>      
    </header>
</template>

<style scoped>
  header {
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 30px 30px 70px 30px;
}

header > p {
  font-size: 20px;
}

header > a {
  width: 300px;
  height: 150px;
  position: relative;
  background: url("../assets/apod.png");
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center;
}

header > a::before {
  content: '';
  z-index: -1;
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  background: inherit;
  border-radius: inherit;
  filter: blur(15px);
  opacity: 0;
  transition: opacity 300ms;
}

a:hover::before {
  opacity: 1;
} 

@media (max-width: 500px) {
  header {
    flex-direction: column;
    text-align: center;
  }
}
</style>