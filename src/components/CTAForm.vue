<script setup>
import TheButton from "@/components/TheButton.vue";
import {nextTick, ref, watchEffect} from "vue";
import {CTAFORM} from "@/constants.js";

const form = ref();

const nameInput = ref();

const phoneValue = ref()
const phoneInput = ref()

watchEffect(() => {
  if (phoneValue.value) {
    const val = phoneDigits();
    const selectionIndex = phoneInput.value.selectionStart
    let newSelectionIndex = 0

    if (phoneValue.value.length !== selectionIndex) {
      newSelectionIndex = phoneInput.value.selectionStart
    }

    phoneValue.value = ['7', '8', '9'].includes(val[0]) ? formatValue(val) : '';

    if (newSelectionIndex) {
      nextTick(() => {
        phoneInput.value.selectionStart = newSelectionIndex;
        phoneInput.value.selectionEnd = newSelectionIndex;

        [[3, 4], [7, 9], [12, 13], [15, 16]].forEach(value => setSelection(value[0], value[1]))

        function setSelection(start, end) {
          if (newSelectionIndex === start || newSelectionIndex === end) {
            phoneInput.value.selectionStart = end
            phoneInput.value.selectionEnd = end
          }
        }
      })
    }
  }

  if (nameInput.value) {
    nameInput.value = 'Петров Петр Петрович xD'.substring(0, nameInput.value.length)
  }
})

function phoneDigits() {
  return phoneValue.value.replace(/\D/g, "")
}

function formatValue(inputValue) {
  let formattedString = '';

  if (inputValue[0] === '9') inputValue = '7' + inputValue;
  const firstSymbols = '+' + inputValue[0].replace(/8/, "7");

  formattedString = firstSymbols + ' ';

  if (inputValue.length > 1) {
    formattedString += '(' + inputValue.substring(1, 4);
  }
  if (inputValue.length >= 5) {
    formattedString += ') ' + inputValue.substring(4, 7);
  }
  if (inputValue.length >= 8) {
    formattedString += '-' + inputValue.substring(7, 9);
  }
  if (inputValue.length >= 10) {
    formattedString += '-' + inputValue.substring(9, 11);
  }

  return formattedString
}

function deleteLastSymbol(e) {
  if (e.keyCode === 8 && phoneDigits().length === 1) phoneValue.value = '';
}

function submitForm() {
  alert(`Молодец ${nameInput.value.trim()}! Ваш номер составил: ${phoneValue.value}!`)
  form.value.reset()
}
</script>

<template>
<form ref="form" class="form" @submit.prevent="submitForm">
  <label class="label">
    <span class="label__span">Ваше имя*</span>
    <input v-model="nameInput" class="label__input" placeholder="Петров Петр" required type="text">
  </label>
  <label class="label">
    <span class="label__span">Ваше номер*</span>
    <input ref="phoneInput" v-model="phoneValue" class="label__input" inputmode="tel"
           minlength="18"
           placeholder="+7 (_ _ _) _ _ _-_ _-_ _" required type="tel" @keydown="deleteLastSymbol">
  </label>
  <TheButton class="submit">Заказать звонок</TheButton>
</form>
</template>

<style lang="scss" scoped>
@use '@/assets/style/variables' as v;

.form {
  display: grid;
  padding: 2rem 4rem;
  background: var(--c-white);
  grid-template-rows: repeat(2, auto) 1fr;
  gap: 1rem;

  @media screen and (max-width: v.$header-tablet) {
    padding: 1rem 2rem;
  }
}

.label {
  display: grid;
  --padding-text: 2rem;
  gap: 0.6rem;

  &__span {
    display: block;
    padding-left: var(--padding-text);
  }

  &__input {
    font-size: 2rem;
    position: relative;
    width: 100%;
    min-height: var(--interactive-height);
    border: 0;
    border-radius: 10px;
    background: #F5F3FF;
    box-shadow: inset 1px 1px 3px 0 rgb(0 0 0 / 0.1);
    padding-inline: var(--padding-text);

    &::placeholder {
      opacity: 1;
      color: #bcbfc4;
    }
  }
}

.submit {
  align-self: end;
  max-width: 100%;

  margin-top: 3rem;
}


</style>
