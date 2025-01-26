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
      <div class="d-none d-md-block col-lg-1"></div>
      <div
        :class="[
          'col-md-3',
          'col-xl-3',
          'col-xxl-2',
          isSidebarVisibleOnMobile ? 'col-12 sidebar-visible-mobile' : 'd-none d-md-block',
        ]"
      >
        <SideBarComponent />
      </div>
      <div :class="['col-md-8', 'col-xl-8', 'col-xxl-7', { 'col-12': !isSidebarVisibleOnMobile }]">
        <ListComponent />
      </div>
      <div class="d-none d-md-block col-xxl-1"></div>
    </div>
  </main>
</template>

<style scoped>
main {
  height: 100%;
  background-color: #fafafc;
  color: #3d424c;
}
</style>
