<template>
  <div class="sideBar">
    <div class="contractType">
      <p>{{ Userdata.contractType }}</p>
    </div>
    <br />
    <div class="userDetails">
      <div>
        <p>Szerződő neve</p>
        <p>{{ Userdata.fullName }}</p>
      </div>
      <div>
        <p>Szerződészám</p>
        <p>{{ Userdata.contractNumber }}</p>
      </div>
      <div>
        <p>Utolsó Befizetés</p>
        <p>{{ latestPaymentDate }}</p>
      </div>
      <div>
        <p>Biztosítási díj rendezve</p>
        <p>{{ insuranceValidUntil }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import userdata from '../../resources/users.json'
import paymentsData from '../../resources/payments.json'

export default {
  components: {},
  data() {
    return {
      Userdata: [],
      latestPaymentDate: '',
      insuranceValidUntil: '',
    }
  },
  mounted() {
    this.loadUserdata()
    this.loadLatestPaymentDatas()

    //console.log('userdata: ', this.Userdata)
  },
  methods: {
    loadUserdata() {
      this.Userdata = userdata[0]
    },
    loadLatestPaymentDatas() {
      if (paymentsData.length > 0) {
        const latestPayment = paymentsData[paymentsData.length - 1]
        this.latestPaymentDate = latestPayment.dateOfPayment
        this.insuranceValidUntil = latestPayment.paymentValidUntil
      } else {
        this.latestPaymentDate = 'Nincs adat'
        this.insuranceValidUntil = 'Nincs adat'
      }
    },
  },
}
</script>

<style>
.contractType {
  padding-top: 24px;
  font-size: larger;
  font-weight: 600;
  color: #283168;
}

.userDetails {
  font-weight: 400;
  color: #3d424c;
}
.userDetails > div {
  margin-bottom: 12px;
  margin-top: 20px;
}
.userDetails > div p {
  margin: 4px 0;
}

.sideBar {
  margin-top: 5px;
  background-color: #ffffff;
  height: 100%;
  padding-left: 20px;
  text-align: left;
  box-shadow: 3px 3px 3px 3px rgb(168, 165, 165);
}
</style>
