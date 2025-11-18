<!-- pages/pinturas_index.vue -->
<template>
  <div class="container pinturas-container">
    <HeaderView />
    <h3 class="page-title">Pinturas</h3>
    <p class="page-subtitle">Esta sección contiene la información sobre las pinturas</p>

    <ContentList path="/pinturas" v-slot="{ list }">
      <div class="pinturas-cards" v-if="list.length">
        <div v-for="p in list" :key="p._path" class="pinturas-card">
          <NuxtLink :to="p._path" class="pinturas-card-link">
            <div style="width: 220px;">
            <h4 class="pinturas-card-title">
              {{ p.titulo || (p._path?.split('/').pop() || '').replace(/-/g,' ') }}
              <small v-if="p.anio" style="font-weight:400; opacity:.8; white-space: nowrap;">({{ p.anio }})</small>
            </h4>
          </div>

            <p v-if="p.tecnica" class="pinturas-card-detail">
              <strong>Técnica:</strong> {{ p.tecnica }}
            </p>

            <ContentQuery
              v-if="p.artistaId"
              path="/artistas"
              :where="{ id: p.artistaId }"
              :only="['nombre','_path']"
              v-slot="{ data: artistas }"
            >
              <p v-if="artistas && artistas.length" class="pinturas-card-detail">
                <strong>Artista:</strong>
                {{ artistas[0].nombre }}
              </p>
            </ContentQuery>

            <ContentQuery
              v-if="p.museoId"
              path="/museos"
              :where="{ id: p.museoId }"
              :only="['nombre','_path']"
              v-slot="{ data: museos }"
            >
              <p v-if="museos && museos.length" class="pinturas-card-detail">
                <strong>Museo:</strong>
                {{ museos[0].nombre }}
              </p>
            </ContentQuery>

            <span class="pinturas-card-cta">Ver más</span>
          </NuxtLink>
        </div>
      </div>
      <p v-else class="pinturas-empty">No se encontraron pinturas.</p>
    </ContentList>

    <FooterView />
  </div>
</template>