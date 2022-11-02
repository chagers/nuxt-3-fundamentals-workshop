<script setup>
</script>

<template>
  <nav class="navbar" role="navigation" aria-label="main navigation">
    <div class="navbar-brand">
      <a class="navbar-item" href="/">
        My Recs
      </a>
    </div>

    <div id="navbarBasicExample" class="navbar-menu">
      <div class="navbar-start">
        
      </div>

      <div class="navbar-end">
        <NuxtLink to="/" class="navbar-item">
          Home
        </NuxtLink>

        <NuxtLink to="/display" class="navbar-item">
          Display
        </NuxtLink>
        
        <div class="navbar-item has-dropdown is-hoverable">
          <a class="navbar-link">
            More
          </a>

          <div class="navbar-dropdown">
            <NuxtLink to="/display/todos" class="navbar-item">ToDos</NuxtLink>
            <NuxtLink to="/display/todos?completed=true" class="navbar-item">Completed ToDos</NuxtLink>
            <NuxtLink to="/display/photos" class="navbar-item">Photos</NuxtLink>
            <NuxtLink to="/display/photos?even=true" class="navbar-item">Even Photos</NuxtLink>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<style>
</style>
