<template>
    <tr>
        <td>{{ paymentId }}</td>
        <td>{{ paymentMethod }}</td>
        <td>{{ dateOfPayment }}</td>
        <td>{{ value }} Ft</td>
        <td>{{ state }}</td>
    </tr>
</template>

<script>
export default {
  props: {
    paymentId: {
      type: Number
     
    },
    paymentMethod: {
      type: String
    },
    dateOfPayment: {
      type: String
    },
    value: {
      type: Number
    },
    state: {
      type: String
    },
  }
};
</script>
