<template>
  <div class="layout">
    <main>
      <h1>Estudio Motix</h1>
      <p>Página en desarrollo</p>
    </main>
  </div>
</template>

<script setup>
import { onMounted } from 'vue';

onMounted(() => {
  function createSnowflake() {
    const snowflake = Object.assign(
      document.createElement('div'),
      {
        className: 'snowflake',
        style: `
        left: ${Math.random() * innerWidth}px;
        top: -5px;
        opacity: ${Math.random()};
        transform: scale(${Math.random() * 1.5 + 0.5});`
      }
    )

    document.body.appendChild(snowflake);

    let posY = -5;
    let speed = Math.random() * 2 + 1;
    let wobble = 0;

    function fall() {
      posY += speed;
      wobble += 0.02;
      snowflake.style.top = posY + 'px';
      snowflake.style.left =
        parseFloat(snowflake.style.left) +
        Math.sin(wobble) * 2 + 'px';

      posY < innerHeight
        ? requestAnimationFrame(fall)
        : snowflake.remove();
    }

    fall();
  }

  function generateSnow() {
    setInterval(createSnowflake, 100);
  }

  generateSnow();
});
</script>

<style>
html,
#__nuxt,
.layout {
  height: 100%;
}

body {
  height: 100%;
  margin: 0;
  padding: 0;
  background-color: black;
  overflow: hidden;
}

.snowflake {
  position: absolute;
  width: 4px;
  height: 4px;
  background-color: white;
  pointer-events: none;
  z-index: 9999;
}

main {
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 1rem;
  position: relative;
  z-index: 1;
  color: white;
  padding: 20px;
}

h1, p {
  text-align: center;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
}

h1 {
  font-size: 1.5rem;
}

p {
  font-size: 1rem;
}
</style>
