<!-- pages/index.vue -->
<template>
 <div class="container">
   <HeaderView />
   <h2 style="margin-top: 15px">Catálogo de Pinturas</h2>
    <p>Este sitio presenta información sobre pinturas famosas, sus artistas y los museos donde se exhiben.</p>
    <ul>
      <li> <NuxtLink to="/museos_index">Museos</NuxtLink></li>
      <li> <NuxtLink to="/pinturas_index">Pinturas</NuxtLink></li>
      <li> <NuxtLink to="/artistas_index">Artistas</NuxtLink></li>
    </ul>
   <FooterView />
 </div>
</template>