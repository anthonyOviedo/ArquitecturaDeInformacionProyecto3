<!-- pages/pinturas/[...slug].vue -->
<template>
  <div class="container pintura-detail">
    <HeaderView />
    
    <ContentDoc v-slot="{ doc }">
      <article class="pintura-detail__article">
        <h2 class="pinturas-detail__title" style="text-align: center;">{{ doc.titulo }}</h2>

        <div class="pinturas-detail__info">
          <ul class="pinturas-detail__meta">
            <ContentQuery
              v-if="doc.museoId"
              path="/museos"
              :where="{ id: doc.museoId }"
              :only="['nombre','_path']"
              v-slot="{ data: museos }"
            >
              <li v-if="museos && museos.length">
                <strong>Museo: </strong>
                <NuxtLink :to="museos[0]._path">{{ museos[0].nombre }}</NuxtLink>
              </li>
            </ContentQuery>
            <ContentQuery
              v-if="doc.artistaId"
              path="/artistas"
              :where="{ id: doc.artistaId }"
              :only="['nombre','_path']"
              v-slot="{ data: artistas }"
            >
              <li v-if="artistas && artistas.length">
                <strong>Artista: </strong>
                <NuxtLink :to="artistas[0]._path">{{ artistas[0].nombre }}</NuxtLink>
              </li>
            </ContentQuery>
            <li v-if="doc.anio"><strong>Año:</strong> {{ doc.anio }}</li>
            <li v-if="doc.tecnica"><strong>Técnica:</strong> {{ doc.tecnica }}</li>
            <li v-if="doc.dimensiones"><strong>Dimensiones:</strong> {{ doc.dimensiones }}</li>
            <li v-if="doc.precio"><strong>Precio:</strong> {{ formatPrice(doc.precio) }}</li>
          </ul>
          
          <ContentRenderer :value="doc" />
        </div>
        <div class="pinturas-detail__media" v-if="doc.imagen" style="text-align: center;">
          <img :src="`/images/${doc.imagen}`" :alt="doc.titulo" style="max-width:700px; width:100%; height:auto; border-radius:8px; display:inline-block;" />
        </div>

        <div class="pinturas-detail__actions" v-if="doc.precio" style="margin-top: 1.5rem; text-align: center;">
          <button
            class="button button-primary snipcart-add-item"
            type="button"
            :data-item-id="doc.id"
            :data-item-name="doc.titulo"
            :data-item-price="Number(doc.precio)"
            :data-item-url="productUrl"
            :data-item-image="doc.imagen ? `/images/${doc.imagen}` : undefined"
          >
            Agregar al carrito
          </button>
        </div>

        <UtterancesComments />
      </article>
    </ContentDoc>

    <FooterView />
  </div>
</template>

<script setup>
const route = useRoute()

const productUrl = computed(() => {
  if (process.client) {
    return new URL(route.path, window.location.origin).toString()
  }
  return route.path
})

const formatPrice = (value) => {
  if (value === undefined || value === null) return ''
  const numeric = Number(value)
  if (Number.isNaN(numeric)) return value
  return new Intl.NumberFormat('es-CO', { style: 'currency', currency: 'USD' }).format(numeric)
}
</script>
