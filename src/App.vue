<template>
  <Header />
  <div class="container"></div>
  <Balance :total="total" />
  <IncomeExpense :income="income" :expenses="expenses"/>
  <TransactionList :transaction="transaction" @transactionDeleted="handelTransactionDeleted"/>
  <AddTransaction @transactionSubmitted="handelTransactionSubmitted"/>
</template>

<script setup>
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpense from "./components/IncomeExpense.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";
import {useToast} from 'vue-toastification';

const toast = useToast();

import {ref,computed} from 'vue';

const transaction = ref([
  { id: 1, text: "flower", amount: -19.99 },
  { id: 2, text: "salary", amount: 299.97 },
  { id: 3, text: "book", amount: -10 },
  { id: 4, text: "camera", amount: 150 },
]);

const total = computed(() => {
  return transaction.value.reduce((acc, t) => acc + t.amount, 0);
});

const income = computed(() => {
  return parseFloat(transaction.value
    .filter(t => t.amount > 0) 
    .reduce((acc, t) => acc + t.amount, 0)
    .toFixed(2));
});

const expenses = computed(() => {
  return parseFloat(transaction.value
    .filter(t => t.amount < 0) 
    .reduce((acc, t) => acc + t.amount, 0)
    .toFixed(2));
});

const handelTransactionSubmitted = (transactiondata) => {
  transaction.value.push({
    id: generateUniqueId(),
    text: transactiondata.text,
    amount: transactiondata.amount,
  });
  toast.success('Transaction added');
};

const generateUniqueId = () => {
  return Math.floor(Math.random() * 10000);
};

const handelTransactionDeleted = (id) => {
  transaction.value = transaction.value.filter(t => t.id !== id);
  toast.success('Transaction Deleted');
};
</script>
