<script setup lang="ts">
import NavbarComponent from './components/NavbarComponent.vue'
import ListComponent from './components/ListComponent.vue'
import SideBarComponent from './components/SideBarComponent.vue'
</script>

<template>
  <header> 
    <div>
      <NavbarComponent/>
    </div>
  </header>

  <main>
    <SideBarComponent/>
    <ListComponent/>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
