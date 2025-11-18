<template>
  <div class="container museos-container">
    <HeaderView />
    <h3 class="page-title">Museos</h3>
    <p class="page-subtitle">Esta sección contiene la información sobre los museos</p>

    <ContentList path="/museos" v-slot="{ list }">
      <div class="museos-cards" v-if="list.length">
        <div v-for="museo in list" :key="museo._path" class="museos-card">
          <NuxtLink :to="museo._path" class="museos-card-link">
            <h4 class="museos-card-title">{{ formatName(museo) }}</h4>
            <p v-if="museo.ubicacion" class="museos-card-detail">
              <strong>Ubicación:</strong> {{ museo.ubicacion }}
            </p>
            <p v-if="museo.fundacion" class="museos-card-detail">
              <strong>Fundación:</strong> {{ museo.fundacion }}
            </p>
            <span class="museos-card-cta">Ver más</span>
          </NuxtLink>
        </div>
      </div>
      <p v-else class="museos-empty">No se encontraron museos.</p>
    </ContentList>

    <FooterView />
  </div>
</template>

<script setup>
const formatName = (museo) => {
  if (!museo) return ''
  if (museo.nombre) return museo.nombre
  if (museo.title) return museo.title

  if (museo._path) {
    const slug = museo._path.split('/').pop() || ''
    if (slug) {
      return slug
        .split('-')
        .map((segment) => segment.charAt(0).toUpperCase() + segment.slice(1))
        .join(' ')
    }
  }

  return 'Museo'
}
</script>
