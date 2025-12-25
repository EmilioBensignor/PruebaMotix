<template>
  <div class="layout">
    <main>
      <h1>¡Dominio en venta!</h1>
      <p>Puedes comprar este dominio en precio promocional esta navidad</p>
      <a
        :href="whatsappUrl"
        target="_blank"
        class="christmas-button"
      >
        🎄 Consultar precio 🎅
      </a>
    </main>
  </div>
</template>

<script setup>
import { onMounted, computed } from 'vue';

const whatsappMessage = "Hola! Soy Lucas Bernath y esto es Jackass";

const whatsappUrl = computed(() => {
  const phone = "5491166411355";
  const message = encodeURIComponent(whatsappMessage);
  return `https://wa.me/${phone}?text=${message}`;
});

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

.christmas-button {
  padding: 15px 30px;
  font-size: 1.2rem;
  font-weight: bold;
  color: white;
  background: linear-gradient(135deg, #c41e3a 0%, #165b33 100%);
  border: 3px solid #ffd700;
  border-radius: 50px;
  text-decoration: none;
  box-shadow: 0 4px 15px rgba(255, 215, 0, 0.4);
  transition: all 0.3s ease;
  cursor: pointer;
  position: relative;
  overflow: hidden;
}

.christmas-button:hover {
  transform: translateY(-3px);
  box-shadow: 0 6px 20px rgba(255, 215, 0, 0.6);
  background: linear-gradient(135deg, #165b33 0%, #c41e3a 100%);
}

.christmas-button:active {
  transform: translateY(-1px);
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
