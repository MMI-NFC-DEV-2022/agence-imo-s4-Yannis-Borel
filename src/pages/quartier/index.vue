<script setup lang="ts">
import { useRouter } from "vue-router/auto";
import { supabase } from "../../supabase";

// const { data, error } = await supabase.from('QuartierCommune').select(
//   *
// );
// const { data, error } = await supabase.from('Quartier').select(`
//   nom_quartier,
//   id,
//   Commune(id, nom_commune)
//   `);
const { data, error } = await supabase.from('Commune').select(`
  *,
  Quartier(*)
  `);
if (error) console.log("n'a pas pu charger la table quartier_commune :", error);


</script>

<template>
  <section class="flex flex-col">
    <h3 class="text-2xl">Liste des quartiers</h3>
    <ul>
      <li v-for="commune in (data)">
        {{ commune.nom_commune }} -
        <ul>
          <li class="pl-3" v-for="quartier in (commune.Quartier)">
           <RouterLink class="text-red-600" :to='{name:"/quartier/edit/[[id]]",params:{id:quartier.id}}'> 
            {{ quartier.nom_quartier }} 
          </RouterLink>
          <RouterLink
            :to='{name:"/quartier/suppr/[[id]]",params:{id:quartier.id}}'
            class="focus-style justify-self-end rounded-md bg-red-500 p-2 shadow-sm">
            Supprimer l'offre
          </RouterLink>
          </li>
        </ul>
      </li>
    </ul>
    
  
  </section>

</template>