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
  data() {
    return {
      isSidebarVisibleOnMobile: false,
    }
  },
  methods: {
    toggleSidebar() {
      this.isSidebarVisibleOnMobile = !this.isSidebarVisibleOnMobile
      //console.log('is sidebarVisible' + this.isSidebarVisibleOnMobile)
    },
  },
}
</script>

<template>
  <header>
    <NavbarComponent @toggleSidebar="toggleSidebar" />
  </header>

  <main class="container-fluid">
    <div class="row">
      <div class="d-none d-md-block col-md-1"></div>
      <div
        :class="[
          'col-md-3',
          isSidebarVisibleOnMobile ? 'col-12 sidebar-visible-mobile' : 'd-none d-md-block',
        ]"
      >
        <SideBarComponent />
      </div>
      <div :class="['col-md-8', { 'col-12': !isSidebarVisibleOnMobile }]">
        <ListComponent />
      </div>
    </div>
  </main>
</template>

<style scoped>
main {
  height: 100%;
  background-color: #fafafc;
}
</style>
