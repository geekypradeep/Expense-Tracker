<template>
    <h3>Add new Transaction</h3>
    <form id="form" @submit.prevent="onSubmit">
        <div class="form-control">
            <label for="text">Text</label>
            <input type="text" id="text" v-model="text" placeholder="Enter Text ..." />
        </div>
        <div class="form-control">
            <label for="amount">Amount<br />(negative-expense , positive-income)</label>
            <input type="text" id="amount" v-model="amount" placeholder="Enter Amount ..." />
        </div>
        <button type="submit" class="btn">Add Transaction</button>
    </form>
</template>

<script setup>
import {ref} from 'vue';
import {useToast} from 'vue-toastification'

const toast = useToast();
const emit = defineEmits(["transactionSubmitted"]);

const text = ref('');
const amount = ref('');

const onSubmit = () => {
    console.log("pradeep");
    if(!text.value || !amount.value)
    {
        toast.error('Both field should be field!');
        return;
    }
    const transactiondata = {
        text:text.value,
        amount:parseFloat(amount.value),
    };

    emit('transactionSubmitted' , transactiondata);

    text.value='';
    amount.value='';
};
</script>