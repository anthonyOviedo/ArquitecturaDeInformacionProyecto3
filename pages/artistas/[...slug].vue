<!-- pages/artistas/[...slug].vue -->
<template>
  <div class="container">
   <HeaderView />
   <div class="row">
     <ContentDoc v-slot="{doc}">
       <div class="three columns">
         <img class="u-max-full-width" :src="'/images/'+doc.imagen">
       </div>
       <div class="six columns">
         <h4>{{doc.nombre}}</h4>
         Nacionalidad: {{doc.nacionalidad}};
         Nacimiento: {{doc.nacimiento}};
         <span v-if="doc.fallecimiento">Fallecimiento: {{doc.fallecimiento}};</span>
         <span v-if="doc.movimientos && doc.movimientos.length">
           Movimientos:
           <span v-for="(m, i) in doc.movimientos" :key="i">
             {{ m }}<span v-if="i < doc.movimientos.length - 1">, </span>
           </span>
         </span>
         <h5>Biografía</h5>
         <ContentRenderer :value="doc" />
         <h5>Pinturas</h5>
         <ul>
           <ContentQuery path="/pinturas" :where="{ artistaId: doc.id }" v-slot="{ data }">
             <li v-for="pintura in data" :key="pintura._path">
               <NuxtLink :to="pintura._path">
                 {{ pintura.titulo }}
                 <span v-if="pintura.anio">({{ pintura.anio }})</span>
               </NuxtLink>
             </li>
           </ContentQuery>
         </ul>

         <UtterancesComments />
       </div>
     </ContentDoc>
   </div>
   <FooterView />
 </div>
</template>
