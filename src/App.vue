<template>
  <div style="padding: 20px; border: 1px solid #ccc; width: 350px; font-family: sans-serif;">
    <h3>Картка студента</h3>

    <div style="margin-bottom: 15px;">
      <label>ПІБ:</label><br />
      <input ref="inputPib" v-model="form.pib" type="text" style="width: 100%;" />
      <div v-if="errors.pib" :style="{ color: errorTypes.pib === 'empty' ? 'orange' : 'red', fontSize: '12px' }">
        {{ errors.pib }}
      </div>
    </div>

    <div style="margin-bottom: 15px;">
      <label>Курс (1-6):</label><br />
      <input ref="inputKurs" v-model="form.kurs" type="number" style="width: 100%;" />
      <div v-if="errors.kurs" :style="{ color: errorTypes.kurs === 'empty' ? 'orange' : 'red', fontSize: '12px' }">
        {{ errors.kurs }}
      </div>
    </div>

    <div style="margin-bottom: 15px;">
      <label>Середній бал (0-100):</label><br />
      <input ref="inputBal" v-model="form.bal" type="number" style="width: 100%;" />
      <div v-if="errors.bal" :style="{ color: errorTypes.bal === 'empty' ? 'orange' : 'red', fontSize: '12px' }">
        {{ errors.bal }}
      </div>
    </div>

    <button @click="perevirka" style="padding: 10px 20px; cursor: pointer;">Зберегти</button>
    
    <p v-if="successMessage" style="color: green; font-weight: bold;">{{ successMessage }}</p>
  </div>
</template>

<script setup>
import { reactive, ref } from 'vue';


const form = reactive({
  pib: "",
  kurs: null,
  bal: null
});

const errors = reactive({
  pib: "",
  kurs: "",
  bal: ""
});

const errorTypes = reactive({
  pib: "",
  kurs: "",
  bal: ""
});

const successMessage = ref("");


const inputPib = ref(null);
const inputKurs = ref(null);
const inputBal = ref(null);

const perevirka = () => {
  Object.keys(errors).forEach(key => (errors[key] = "", errorTypes[key] = ""));
  successMessage.value = "";
  const rules = [
    {
      field: 'pib',
      ref: inputPib,
      check: () => !form.pib,
      message: "Це поле треба обов'язково заповнити!",
      type: 'empty'
    },
    {
      field: 'kurs',
      ref: inputKurs,
      check: () => form.kurs === null || form.kurs === "",
      message: "Вкажіть курс студента!",
      type: 'empty'
    },
    {
      field: 'kurs',
      ref: inputKurs,
      check: () => form.kurs < 1 || form.kurs > 6,
      message: "Курс має бути тільки від 1 до 6",
      type: 'invalid'
    },
    {
      field: 'bal',
      ref: inputBal,
      check: () => form.bal === null || form.bal === "",
      message: "Вкажіть середній бал!",
      type: 'empty'
    },
    {
      field: 'bal',
      ref: inputBal,
      check: () => form.bal < 0 || form.bal > 100,
      message: "Бал не може бути менше 0 або більше 100!",
      type: 'invalid'
    }
  ];

  const firstError = rules.find(rule => rule.check());

  if (firstError) {
    errors[firstError.field] = firstError.message;
    errorTypes[firstError.field] = firstError.type;
    firstError.ref.value.focus();
    return;
  }

  successMessage.value = "Студента успішно додано!";
};
</script>