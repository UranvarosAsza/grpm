<template>
  <nav class="navbar">
    <div class="container-fluid">
      <div class="row w-100 align-items-center">
        <div class="d-none d-md-block col-md-1"></div>
        <div class="col">
          <span class="navbar-brand">
            <img class="logo" src="../../resources/images/logo.png" />
          </span>
        </div>
        <div class="col-auto">
          <button class="btn sideBarInMobile d-md-none" @click="$emit('toggleSidebar')">
            <img src="../../resources/images/three-dots.svg" alt="Menu" />
          </button>
          <button class="btn">
            <img src="../../resources/images/arrow-right-circle.svg" /> Kilépés
          </button>
        </div>
      </div>
    </div>
  </nav>
</template>

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

<style>
.sideBarInMobile {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background-color: #f1f2f4;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0;
  border: none;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.sideBarInMobile img {
  width: 20px;
  height: 20px;
}

.navbar .col-auto {
  display: flex;
  align-items: center;
  justify-content: flex-end;
  gap: 10px;
}

.navbar .btn {
  margin-left: 0;
}

.logo {
  height: 34px;
}
.navbar {
  background-color: #ffffff;
  color: #0a113d;
  height: 80px;
  box-shadow: 2px 2px 5px rgb(168, 165, 165);
  width: 100%;
}
</style>
