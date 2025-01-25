<template>
  <div class="list">
    <h2>Fizetési előzmények</h2>
    <table>
      <thead>
        <tr>
          <th>Azonosító</th>
          <th>Befizetés módja</th>
          <th>Dátum</th>
          <th>Összeg</th>
          <th>Státusz</th>
          <th>(gombok)</th>
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
    //console.log(this.Payments)
  },
  methods: {
    loadPayments() {
      this.Payments = paymentsData
    },
  },
}
</script>

<style>
list {
  background-color: #fafafc;
}
</style>
