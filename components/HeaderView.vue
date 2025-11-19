<template>
  <nav class="main-nav">
    <NuxtLink class="nav-item button button-primary" to="/">Inicio</NuxtLink>
    <NuxtLink class="nav-item button button-primary" to="/pinturas_index">Pinturas</NuxtLink>
    <NuxtLink class="nav-item button button-primary" to="/artistas_index">Artistas</NuxtLink>
    <NuxtLink class="nav-item button button-primary" to="/museos_index">Museos</NuxtLink>
    <button class="nav-item button button-primary snipcart-checkout" type="button">
      Carrito
    </button>
  </nav>
</template>

<style scoped>
.main-nav {
  margin-top: 15px;
  display: grid;
  gap: 10px;
  grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
}

.nav-item {
  text-align: center;
  width: 100%;
}

@media (min-width: 768px) {
  .main-nav {
    grid-template-columns: repeat(5, 1fr);
  }
}
</style>