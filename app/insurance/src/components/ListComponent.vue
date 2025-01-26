<template>
  <div class="list">
    <div class="selector">
      <p class="notactivated">Fizetendő tételek</p>
      <p class="notactivated">Eseti díj befizetése</p>
      <p class="activated">Fizetési előzmények</p>
    </div>
    <table>
      <thead>
        <tr>
          <th><div class="header">Azonosító</div></th>
          <th><div class="header">Befizetés módja</div></th>
          <th><div class="header">Dátum</div></th>
          <th><div class="header">Összeg</div></th>
          <th><div class="header">Státusz</div></th>
          <th><div class="header"></div></th>
        </tr>
      </thead>
      <tbody>
        <ListElement
          v-for="payment in Payments"
          :key="payment.paymentId"
          :paymentId="payment.paymentId"
          :paymentMethod="payment.paymentMethod"
          :dateOfPayment="payment.dateOfPayment"
          :value="payment.value"
          :state="payment.state"
          :attachmentId="payment.attachmentId"
          :paymentValidUntil="payment.paymentValidUntil"
        />
      </tbody>
    </table>
  </div>
</template>

<script>
import paymentsData from '../../resources/payments.json'
import ListElement from './ListElement.vue'

export default {
  components: {
    ListElement,
  },
  data() {
    return {
      Payments: [],
    }
  },
  mounted() {
    this.loadPayments()
    console.log(this.Payments)
  },
  methods: {
    loadPayments() {
      this.Payments = paymentsData
    },
  },
}
</script>

<style>
table {
  border-collapse: separate;
  border-spacing: 0 16px;
}
.header {
  margin-bottom: 16px;
}
.selector p {
  font-size: 16px !important;
  display: inline;
  margin-left: 15px;
  margin-right: 15px;
}
.selector {
  padding-top: 40px;
  padding-bottom: 30px;
}
.list {
  background-color: #fafafc;
}
.activated {
  font-size: 14px;
  font-weight: 600;
  color: #283168;
}
.notactivated {
  font-size: 14px;
  font-weight: 400;
  color: #283168;
}
table {
  width: 100%;
}
th {
  color: #6f7381;
  font-weight: 400;
}
</style>
