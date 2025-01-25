<template>
  <div class="sideBar">
    <div class="contractType">
      <h3>alma kutya</h3>
    </div>
    <div class="userDetails">
      <p>Szerződő neve</p>
      <p>{{ Userdata.fullName }}</p>
      <p>Szerződészám</p>
      <p>{{ Userdata.contractNumber }}</p>
      <p>Utolsó Befizetés</p>
      <p>abrakadabra</p>
    </div>
  </div>

  <!-- {{ Userdata.contractType }}</h3> -->
</template>

<script>
import userdata from '../../resources/users.json'
import paymentsData from '../../resources/payments.json'

export default {
  components: {},
  data() {
    return {
      Userdata: [],
    }
  },
  mounted() {
    this.loadUserdata()
    //console.log('userdata: ', this.Userdata)
  },
  methods: {
    loadUserdata() {
      this.Userdata = userdata[0]
    },
  },
}
</script>

<style>
.contractType {
  font-weight: 600;
  color: #283168;
}

.userDetails {
  font-weight: 400;
  color: #3d424c;
}
.sideBar {
  padding-left: 20px;
  text-align: left;
}
</style>
