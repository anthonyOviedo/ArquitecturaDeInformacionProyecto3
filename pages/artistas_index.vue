<template>
  <div class="container artistas-container">
    <HeaderView />
    <h3 class="page-title">Artistas</h3>
    <p class="page-subtitle">Esta sección contiene la información sobre los artistas</p>

    <ContentList path="/artistas" v-slot="{ list }">
      <div class="artistas-cards" v-if="list.length">
        <div v-for="artista in list" :key="artista._path" class="artistas-card">
          <NuxtLink :to="artista._path" class="artistas-card-link">
            <h4 class="artistas-card-title">{{ formatName(artista) }}</h4>

            <p v-if="artista.nacionalidad" class="artistas-card-detail">
              <strong>Nacionalidad:</strong> {{ artista.nacionalidad }}
            </p>

            <p v-if="artista.nacimiento" class="artistas-card-detail">
              <strong>Nacimiento:</strong> {{ artista.nacimiento }}
            </p>

            <p v-if="artista.fallecimiento" class="artistas-card-detail">
              <strong>Fallecimiento:</strong> {{ artista.fallecimiento }}
            </p>

            <p v-if="hasMovimientos(artista)" class="artistas-card-detail">
              <strong>Movimiento:</strong> {{ formatMovimientos(artista.movimientos) }}
            </p>

            <span class="artistas-card-cta">Ver más</span>
          </NuxtLink>
        </div>
      </div>
      <p v-else class="artistas-empty">No se encontraron artistas.</p>
    </ContentList>

    <FooterView />
  </div>
</template>

<script setup>
const formatName = (artista) => {
  if (!artista) return ''
  if (artista.nombre) return artista.nombre
  if (artista.title) return artista.title

  if (artista._path) {
    const slug = artista._path.split('/').pop() || ''
    if (slug) {
      return slug
        .split('-')
        .map((s) => s.charAt(0).toUpperCase() + s.slice(1))
        .join(' ')
    }
  }
  return 'Artista'
}

// Helpers para movimientos
const hasMovimientos = (a) =>
  !!a && (Array.isArray(a.movimientos) ? a.movimientos.length > 0 : !!a.movimientos)

const formatMovimientos = (movs) => {
  if (Array.isArray(movs)) {
    // muestra hasta 2
    return movs.slice(0, 2).join(', ')
  }
  return movs || ''
}
</script>
