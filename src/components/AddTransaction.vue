<template>
  <h3>Add new transaction</h3>
  <form id="form" @submit.prevent="addTransaction">
    <div class="form-control">
      <label for="text">Text</label>
      <input type="text" id="text" v-model="text" placeholder="Enter text..." />
    </div>
    <div class="form-control">
      <label for="amount">
        Amount
        <br />
        (negative - expense, positive - income)
      </label>
      <input
        type="text"
        id="amount"
        v-model="amount"
        placeholder="Enter amount..."
      />
    </div>
    <button type="submit" class="btn">Add transaction</button>
  </form>
</template>
<script setup>
import { ref } from "vue";
import { useToast } from "vue-toastification";

const text = ref("");
const amount = ref("");

const toast = useToast();
const emit = defineEmits(["transactionSubmitted"]);

const addTransaction = () => {
  if (!text.value || !amount.value) {
    toast.error("Both fields are required!");
    return;
  } else if (!parseFloat(amount.value)) {
    toast.error("Error on the entering amount!");
    return;
  }

  const transactionData = {
    text: text.value,
    amount: parseFloat(amount.value),
  };

  emit("transactionSubmitted", transactionData);

  text.value = "";
  amount.value = "";
};
</script>
