<template>
  <tr class="payment">
    <td>{{ paymentId }}</td>
    <td>
      <span v-if="paymentMethod === 'card'">Bankkártya</span>
      <span v-else-if="paymentMethod === 'transaction'">Átutalás</span>
      <span v-else>Ismeretlen</span>
    </td>
    <td>{{ dateOfPayment }}</td>
    <td class="value">{{ value }} Ft</td>
    <td>
      <span v-if="state === 'Ongoing'" class="status ongoing">
        <span class="dot gray"></span> Folyamatban
      </span>
      <span v-else-if="state === 'Succesfull'" class="status succesfull">
        <span class="dot green"></span> Beérkezett
      </span>
      <span v-else-if="state === 'Unsuccesfull'" class="status unsuccesfull">
        <span class="dot red"></span> Sikertelen
      </span>
    </td>
    <td>
      <button
        class="btn btn-primary"
        :data-bs-target="'#collapse-' + paymentId"
        data-bs-toggle="collapse"
      >
        Részletek
      </button>
    </td>
  </tr>
  <tr class="details">
    <td colspan="6" class="collapse py-2" :id="'collapse-' + paymentId">
      <div>Ez a toggle-álható tartalom!</div>
    </td>
  </tr>
  <tr class="attachment">
    <td colspan="6" class="collapse py-2" :id="'collapse-' + paymentId">
      <div>Csatolmány</div>
      <div>
        <a href="../../resources/documents/CsatolmányPélda.pdf" download>
          <img src="../../resources/images/file-earmark-pdf-fill.svg" /> Fizetési nyugta letöltése
        </a>
      </div>
    </td>
  </tr>
</template>

<script>
export default {
  props: {
    paymentId: {
      type: Number,
    },
    paymentMethod: {
      type: String,
    },
    dateOfPayment: {
      type: String,
    },
    value: {
      type: Number,
    },
    state: {
      type: String,
    },
  },
}
</script>

<style>
.attachment div {
  padding-left: 20px;
}
.details div {
  padding-left: 20px;
}
.attachment {
  box-shadow: 3px 3px 3px 3px rgb(168, 165, 165);
  background-color: #ffffff;
}
.details {
  box-shadow: 3px 3px 3px 3px rgb(168, 165, 165);
  background-color: #ffffff;
}
.payment {
  margin-left: 25px;
  margin-bottom: 16px !important;
  height: 79px;
  background-color: #ffffff;
  box-shadow: 3px 3px 3px 3px rgb(168, 165, 165);
}
.payment > td {
  padding-left: 20px;
  text-align: left;
  margin-bottom: 16px;
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
