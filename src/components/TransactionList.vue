<template>
  <h3>History</h3>
  <ul v-if="transactions?.length" id="list" class="list">
    <li
      v-for="transaction in transactions"
      v-bind:key="transaction.id"
      :class="transaction.amount < 0 ? 'minus' : 'plus'"
    >
      {{ transaction.text }}
      <span>${{ transaction.amount }}</span>
      <button @click="deleteTransaction(transaction.id)" class="delete-btn">
        x
      </button>
    </li>
  </ul>
  <p v-else style="opacity: 0.5">There isn't any transactions</p>
</template>
<script setup>
import { defineProps } from "vue";

const props = defineProps({
  transactions: {
    type: Array,
    required: true,
  },
});
const emit = defineEmits(["deleteTransaction"]);

const deleteTransaction = (id) => {
  emit("deleteTransaction", id);
};
</script>
