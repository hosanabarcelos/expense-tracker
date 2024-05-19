<template>
  <h3>Nova transação</h3>
  <form id="form" @submit.prevent="onSubmit">
    <div class="form-control">
      <label for="text">O que é?</label>
      <input type="text" id="text" placeholder="Adicione o que entrou ou saiu" v-model="text" />
    </div>
    <div class="form-control">
      <label for="amount"
        >Valor <br />
      </label
      >
      <input
        type="text"
        id="amount"
        placeholder="Adicione o valor"
        v-model="amount"
      />
    </div>
    <button class="btn">Nova transação</button>
  </form>
</template>

<script setup>
import { useToast } from 'vue-toastification';
import { ref } from 'vue';

const text = ref('');
const amount = ref('');

const toast = useToast();

const emit = defineEmits(['transactionSubmitted']);

const onSubmit = () => {
  if (!text.value || !amount.value) {
    toast.error('Informe os dados da sua transação.');
    return;
  }

  const transactionData = {
    text: text.value,
    amount: parseFloat(amount.value),
  };

  emit('transactionSubmitted', transactionData);

  text.value = '';
  amount.value = '';
};
</script>
