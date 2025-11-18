<template>
  <ClientOnly>
    <section class="comments-section" style="margin-top: 2rem;">
      <h3 style="margin-bottom: 1rem;">Comentarios</h3>
      <component
        :is="'script'"
        src="https://utteranc.es/client.js"
        repo="anthonyOviedo/AdeInformacionTarea4"
        issue-term="pathname"
        theme="github-light"
        crossorigin="anonymous"
        async
      ></component>
    </section>
  </ClientOnly>
</template>

<script setup>
</script>
