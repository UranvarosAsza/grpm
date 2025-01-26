<template>
  <tr class="payment d-none d-md-table-row">
    <td>
      <button class="btn">
        <img src="../../resources/images/chevron-right.svg" />
      </button>
      {{ paymentId }}
    </td>
    <td>{{ paymentMethodDisplay }}</td>
    <td>{{ dateOfPayment }}</td>
    <td class="value">{{ new Intl.NumberFormat('hu-HU').format(value) }} Ft</td>
    <td><span :class="stateClass"></span> {{ stateDisplay }}</td>
    <td class="buttons">
      <span>
        <img v-if="hasAttachmentData" src="../../resources/images/attachment.png" />
        <img
          v-else
          src="data:image/gif;base64,R0lGODlhAQABAAD/ACwAAAAAAQABAAACADs="
          style="width: 17px; height: 17px"
          alt="Placeholder"
        />
      </span>

      <button class="btn" @click="toggleDetails" :aria-expanded="isOpen">
        <img v-if="isOpen" src="../../resources/images/chevron-up.svg" />
        <img v-else src="../../resources/images/chevron-down.svg" />
      </button>
    </td>
  </tr>
  <tr v-if="isOpen" class="details d-none d-md-table-row">
    <td colspan="6" class="py-2">
      <table class="subtable">
        <thead>
          <tr>
            <th>Biztosítási időszak</th>
            <th>Díjelőírás</th>
            <th>Könyvelt díj</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>{{ dateOfPayment }} - {{ paymentValidUntil }}</td>
            <td>{{ new Intl.NumberFormat('hu-HU').format(value) }}</td>
            <td class="value">{{ new Intl.NumberFormat('hu-HU').format(value) }}</td>
          </tr>
        </tbody>
      </table>
    </td>
  </tr>
  <tr v-if="isOpen & hasAttachmentData" class="attachment d-none d-md-table-row">
    <td colspan="6" class="py-2">
      <div>Csatolmány</div>
      <div>
        <a href="../../resources/documents/CsatolmányPélda.pdf" download>
          <img src="../../resources/images/file-earmark-pdf-fill.svg" />
          Fizetési nyugta letöltése
        </a>
      </div>
    </td>
  </tr>

  <div class="mobilePayment d-block d-md-none shadow-sm rounded bg-white p-3">
    <div class="d-flex align-items-center justify-content-between">
      <div class="mobileDot">
        <span :class="stateClass"></span>
      </div>

      <div class="mobileData text-center">
        <p>{{ stateDisplay }}</p>
        <p class="value">{{ new Intl.NumberFormat('hu-HU').format(value) }} Ft</p>
        <p>
          Fizetési dátum {{ dateOfPayment }}
          <span>
            <img v-if="hasAttachmentData" src="../../resources/images/attachment.png" />
            <img
              v-else
              src="data:image/gif;base64,R0lGODlhAQABAAD/ACwAAAAAAQABAAACADs="
              style="width: 17px; height: 17px"
              alt="Placeholder"
            />
          </span>
        </p>
      </div>

      <div class="mobileButton">
        <button class="btn" @click="toggleDetails" :aria-expanded="isOpen">
          <img v-if="isOpen" src="../../resources/images/chevron-up.svg" />
          <img v-else src="../../resources/images/chevron-down.svg" />
        </button>
      </div>
    </div>
  </div>
  <div v-if="isOpen" class="mobileDetails d-block d-md-none shadow-sm rounded bg-white p-3">
    <div>
      <p>Státusz</p>
      <p>{{ stateDisplay }}</p>
    </div>
    <div>
      <p>Azonosító</p>
      <p>{{ paymentId }}</p>
    </div>
    <div>
      <p>Hogyan</p>
      <p>{{ paymentMethodDisplay }}</p>
    </div>
  </div>
  <div
    v-if="isOpen & hasAttachmentData"
    class="mobileAttachment d-block d-md-none shadow-sm rounded bg-white p-3"
  >
    <div>Csatolmány</div>
    <div class="attachmentContent">
      <img class="icon" src="../../resources/images/file-earmark-pdf-fill.svg" />
      <p>Fizetési nyugta letöltése</p>
      <a class="downloadIcon" href="../../resources/documents/CsatolmányPélda.pdf" download>
        <img src="../../resources/images/download.svg" />
      </a>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    paymentId: Number,
    paymentMethod: String,
    dateOfPayment: String,
    value: Number,
    state: String,
    hasAttachment: Boolean,
    attachmentId: Number,
    paymentValidUntil: String,
  },
  data() {
    return {
      isOpen: false,
    }
  },
  computed: {
    paymentMethodDisplay() {
      return this.paymentMethod === 'card'
        ? 'Bankkártya'
        : this.paymentMethod === 'transaction'
          ? 'Átutalás'
          : 'Egyéb'
    },
    stateDisplay() {
      return this.state === 'Ongoing'
        ? 'Folyamatban'
        : this.state === 'Succesfull'
          ? 'Beérkezett'
          : 'Sikertelen'
    },
    stateClass() {
      return {
        dot: true,
        gray: this.state === 'Ongoing',
        green: this.state === 'Succesfull',
        red: this.state === 'Unsuccesfull',
      }
    },
    hasAttachmentData() {
      return !!this.attachmentId
    },
  },
  mounted() {
    // console.log(this.attachmentId)
  },
  methods: {
    toggleDetails() {
      this.isOpen = !this.isOpen
    },
  },
}
</script>

<style>
/*Mobile view */
.mobilePayment,
.mobileAttachment,
.mobileDetails {
  width: 100%;

  display: flex;
  background-color: white;
  box-shadow: 2px 2px 5px rgb(168, 165, 165);
  border-radius: 5px;
  margin-left: 15px;
  margin-bottom: 16px;
  margin-right: 15px;
}

.mobilePayment .mobileDot {
  flex: 0 0 auto;
  margin-right: 1rem;
}

.mobilePayment .mobileDot span {
  display: inline-block;
  width: 16px;
  height: 16px;
  border-radius: 50%;
}

.mobilePayment .mobileData {
  flex: 1;
}

.mobilePayment .mobileData p {
  margin: 0;
  line-height: 1.5;
  font-size: 0.9rem;
  text-align: left;
}

.mobilePayment .mobileData .value {
  font-weight: bold;
  font-size: 1rem;
}

.mobilePayment .mobileButton {
  flex: 0 0 auto;
  margin-left: auto;
}

.mobilePayment .mobileButton .btn {
  background: none;
  border: none;
  padding: 0;
}

.mobilePayment .mobileButton img {
  width: 20px;
  height: 20px;
}
.mobileDetails div p:nth-of-type(1) {
  font-size: 12px;
  margin-bottom: 2px;
}

.mobileDetails div p:nth-of-type(2) {
  font-size: 14px;
  margin-bottom: 20px;
}
.mobileDetails div:last-of-type p:nth-of-type(2) {
  margin-bottom: 0;
}

.mobileAttachment .attachmentContent {
  display: flex;
  justify-content: space-between;
  text-align: left;
}

.mobileAttachment .attachmentContent p {
  margin: 0;
  font-size: 14px !important;
}

/*Desktop view  */
.subtable td,
th {
  padding-left: 20px;
}
.attachment div,
.details div {
  padding-left: 20px;
}

.attachment,
.details {
  border-radius: 5px;
  box-shadow: 2px 2px 5px rgb(168, 165, 165);
  background-color: #ffffff;
}

.payment {
  border-radius: 5px;
  margin-left: 25px;
  margin-bottom: 16px !important;
  height: 79px;
  background-color: #ffffff;
  box-shadow: 2px 2px 5px rgb(168, 165, 165);
}
.payment > td {
  padding-left: 20px;
  text-align: left;
  margin-bottom: 16px;
}
.payment p,
span {
  font-size: 14px;
}
.buttons {
  align-items: right;
}
.status {
  display: flex;
  align-items: center;
  gap: 8px;
}
.dot {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  display: inline-block;
}
.dot.gray {
  background-color: #a1caff;
}

.dot.green {
  background-color: #01bba1;
}

.dot.red {
  background-color: #dc414f;
}
.value {
  font-weight: bold;
}
</style>
