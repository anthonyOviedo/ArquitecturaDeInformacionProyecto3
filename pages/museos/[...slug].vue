<template>
  <div class="container museo-detail">
    <HeaderView />
    <ContentDoc v-slot="{ doc }">
      <article class="museo-detail__article">
        <div v-if="doc?.imagen" class="museo-detail__media">
          <img
            :src="resolveImage(doc.imagen)"
            :alt="formatName(doc)"
            class="museo-detail__image"
          />
        </div>

        <div class="museo-detail__content">
          <h2 class="museo-detail__title">{{ formatName(doc) }}</h2>
          <ul class="museo-detail__meta">
            <li v-if="doc?.ubicacion">
              <strong>Ubicación:</strong> {{ doc.ubicacion }}
            </li>
            <li v-if="doc?.fundacion">
              <strong>Fundación:</strong> {{ doc.fundacion }}
            </li>
          </ul>

          <ContentRenderer :value="doc" />

          <section class="museo-detail__obras">
            <h3>Obras exhibidas</h3>
            <ContentQuery
              path="/pinturas"
              :where="{ museoId: doc.id }"
              :only="['titulo','_path','anio']"
              v-slot="{ data }"
            >
              <ul v-if="data && data.length">
                <li v-for="obra in data" :key="obra._path">
                  <NuxtLink :to="obra._path">{{ obra.titulo }}</NuxtLink>
                  <span v-if="obra.anio"> ({{ obra.anio }})</span>
                </li>
              </ul>
              <p v-else>No se encontraron obras en este museo.</p>
            </ContentQuery>
          </section>

          <UtterancesComments />
        </div>
      </article>
    </ContentDoc>
    <FooterView />
  </div>
</template>

<script setup>
const formatName = (doc) => {
  if (!doc) return 'Museo'
  return doc.nombre || doc.title || 'Museo'
}

const resolveImage = (path) => {
  if (!path) return ''
  const normalized = String(path).replace(/^\/+/, '')
  return `/images/${normalized}`
}
</script>
