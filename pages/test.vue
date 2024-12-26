<script setup>
import { ref } from 'vue';

// Estado reactivo para los valores de los inputs OTP
const otp = ref(Array(6).fill('')); // Array para los 6 dígitos del OTP
const inputRefs = ref([]); // Referencias para los inputs individuales

// Función para enfocar el siguiente input automáticamente
const focusNext = (index) => {
  if (otp.value[index] && index < otp.value.length - 1) {
    inputRefs.value[index + 1]?.focus();
  }
};

// Función para enfocar el input previo al borrar con backspace
const focusPrev = (index) => {
  if (!otp.value[index] && index > 0) {
    inputRefs.value[index - 1]?.focus();
  }
};

// Función para enviar el OTP
const submitOtp = () => {
  const enteredOtp = otp.value.join('');
  console.log('OTP ingresado:', enteredOtp);
  // Aquí puedes añadir lógica de envío o validación
};
</script>
<template>
<div class="otp-container">
    <label for="otp-inputs">One-Time Password</label>
    <div id="otp-inputs" class="otp-inputs">
      <input
        v-for="(value, index) in otp"
        :key="index"
        type="number"
        maxlength="1"
        :ref="el => (inputRefs[index] = el)"
        v-model="otp[index]"
        @input="focusNext(index)"
        @keydown.backspace="focusPrev(index)"
      />
    </div>
    <p>Por favor, introduce el código OTP enviado a tu email</p>
    <button @click="submitOtp">Enviar</button>
  </div>
</template>
<style scoped>
.otp-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  color: #f1f1f1; /* Texto claro en fondo oscuro */
  font-family: Arial, sans-serif;
  background-color: #121212; /* Fondo oscuro */
  padding: 20px;
  border-radius: 8px;
}
label {
  margin-bottom: 10px;
  font-size: 1.2em;
  font-weight: bold;
}

.otp-inputs {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-bottom: 10px;
}

.otp-inputs input {
  width: 50px;
  height: 50px;
  text-align: center;
  font-size: 1.5em;
  border: 1px solid #333;
  background-color: #1e1e1e;
  color: #f1f1f1;
  border-radius: 5px;
  outline: none;
}

.otp-inputs input:focus {
  border-color: #ffffff;
  background-color: #2a2a2a;
}

p {
  margin-bottom: 20px;
  font-size: 0.9em;
}

button {
  background-color: #ffffff;
  color: #121212;
  border: none;
  padding: 10px 20px;
  font-size: 1em;
  font-weight: bold;
  cursor: pointer;
  border-radius: 5px;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #e0e0e0;
}
</style>
