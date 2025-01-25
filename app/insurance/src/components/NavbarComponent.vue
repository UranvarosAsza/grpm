<script>
export default {
  props: {
    isSidebarVisible: {
      type: Boolean,
      required: true,
    },
  },
}
</script>

<template>
  <nav class="navbar">
    <div class="container-fluid">
      <span class="navbar-brand"><img class="logo" src="../../resources/images/logo.png" /></span>
      <span>
        <button class="btn">
          <img src="../../resources/images/arrow-right-circle.svg" /> Kilépés
        </button>
      </span>
    </div>
  </nav>
</template>

<style>
.logo {
  height: 34px;
}
.navbar {
  background-color: #ffffff;
  color: #0a113d;
  height: 80px;
  box-shadow:
    5px,
    5px gray;
  width: 100%;
}
</style>
