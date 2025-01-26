<template>
  <tr class="payment">
    <td>
      <button class="btn">
        <img src="../../resources/images/chevron-right.svg" />
      </button>
      {{ paymentId }}
    </td>
    <td>{{ paymentMethodDisplay }}</td>
    <td>{{ dateOfPayment }}</td>
    <td class="value">{{ value }} Ft</td>
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
        <img v-else src="../../resources//images/chevron-down.svg" />
      </button>
    </td>
  </tr>
  <tr v-if="isOpen" class="details">
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
            <td>{{ value }}</td>
            <td class="value">{{ value }}</td>
          </tr>
        </tbody>
      </table>
    </td>
  </tr>
  <tr v-if="isOpen & hasAttachmentData" class="attachment">
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
  box-shadow: 2px 2px 5px rgb(168, 165, 165);
  background-color: #ffffff;
}

.payment {
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
