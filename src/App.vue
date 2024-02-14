<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <h1>Test</h1>

    <nav class="*:text-red-500 flex flex-col">
      <RouterLink to="/">Home</RouterLink>
      <RouterLink to="/about">About</RouterLink>
      <RouterLink to="/simple">Simple</RouterLink>
      <RouterLink to="/maisons">Maison</RouterLink>
      <RouterLink to="/maisons/edit">Créer des maison</RouterLink>
      <RouterLink to="/login-logout">Connexion</RouterLink>
      <RouterLink to="/quartier">Quartier</RouterLink>
      <RouterLink to="/quartier/edit">Nouveau Quartier</RouterLink>
    </nav>
  </header>
  <Suspense> 
    <RouterView :key="$router.params"/>
  </Suspense>
</template>