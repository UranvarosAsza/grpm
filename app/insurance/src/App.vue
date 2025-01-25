<script>
import NavbarComponent from './components/NavbarComponent.vue'
import SideBarComponent from './components/SideBarComponent.vue'
import ListComponent from './components/ListComponent.vue'

export default {
  components: {
    ListComponent,
    NavbarComponent,
    SideBarComponent,
  },
}
</script>

<template>
  <header>
    <NavbarComponent />
  </header>

  <main class="container-fluid">
    <div class="row">
      <!-- SideBarComponent: 3 oszlop széles minden nézeten nagyobb mint mobil -->
      <div class="col-md-4 d-none d-md-block">
        <SideBarComponent />
      </div>
      <!-- ListComponent: 8 oszlop széles, mobilon 12 -->
      <div class="col-md-8 col-12">
        <ListComponent />
      </div>
    </div>
  </main>
</template>

<style scoped>
main {
  background-color: #fafafc;
}
</style>
