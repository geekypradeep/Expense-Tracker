<template>
    <div v-if="transaction.length">
        <h3>History</h3>
            <ul id="list" class="list">
                <li
                v-for="t in transaction"
                :key="t.id"
                :class="t.amount < 0 ? 'minus' : 'plus'"
                >
                {{ t.text }} <span>{{ t.amount }}</span>
                <button @click="deleteTransaction(t.id)" class="delete-btn">x</button>
                </li>
            </ul>
    </div>
  
</template>

<script setup>
import { defineProps } from "vue";

const emit = defineEmits(["transactionDeleted"]);

const props = defineProps({
  transaction: {
    type: Array,
    required: true,
  },
});

const deleteTransaction = (id) => {
  emit("transactionDeleted", id);
};
</script>
