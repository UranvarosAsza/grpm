<template>
  <tr>
    <td>{{ paymentId }}</td>
    <td>{{ paymentMethod }}</td>
    <td>{{ dateOfPayment }}</td>
    <td>{{ value }} Ft</td>
    <td>{{ state }}</td>
    <td>
      <button class="btn btn-primary" data-bs-target="#collapseTarget" data-bs-toggle="collapse">
        részletek
      </button>
    </td>
  </tr>
  <tr>
    <td class="collapse py-2" id="collapseTarget">This is the toggle-able content!</td>
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
