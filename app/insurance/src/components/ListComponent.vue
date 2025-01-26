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
@media (max-width: 768px) {
  .selector {
    text-align: center;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    max-height: 60px;
    font-size: 14px;
  }
  .selector p {
    flex: 1 1;
    text-align: center;
    margin: 0;
    word-wrap: break-word;
    white-space: normal;
  }
  .activated,
  .notactivated {
    padding-bottom: 15px !important;
  }
  .activated {
    border-bottom: 3px solid #01bba1;
  }
  table th {
    display: none;
  }
}

table {
  width: 100%;
  border-collapse: separate;
  border-spacing: 0 16px;
}

.header {
  margin-bottom: 16px;
}

.selector {
  background-color: #ffffff;
  padding: 40px 0 30px;
  border-bottom: 3px solid #f1f2f4;
}

.selector p {
  font-size: 16px;
  display: inline;
  margin: 0 15px;
}

.list {
  background-color: #fafafc;
}

.activated,
.notactivated {
  font-size: 14px;
  font-weight: 400;
  color: #283168;
  padding-bottom: 30px;
  border-bottom: 3px solid #f1f2f4;
}

.activated {
  font-weight: 600;
  border-bottom: 3px solid #01bba1;
}

th {
  color: #6f7381;
  font-weight: 400;
}
</style>
