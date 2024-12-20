<script setup>
import {PHONE} from "@/constants.js";
import {computed} from "vue";

const formattedPhone = computed(() => {
  const numbers = [...PHONE.match(/(\d)(\d{3})(\d{3})(\d{2})(\d{2})/)].slice(1);
  if (numbers[0] !== 8) numbers[0] = '+' + numbers[0];
  return `${numbers[0]} (${numbers[1]}) <b>${numbers[2]}-${numbers[3]}-${numbers[4]}</b>`;
})

</script>

<template>
<a :href="'tel:'+PHONE" class="phone">
  <span class="phone__icon"></span>
  <span class="phone__text" v-html="formattedPhone"></span>
</a>
</template>

<style lang="scss" scoped>
@use '@/assets/style/variables' as v;

.phone {
  flex-shrink: 3;
  display: flex;
  align-items: center;
  flex-basis: 21rem;
  justify-content: flex-end;
  container: phone / inline-size;
  gap: 1rem;
  padding: 0.2rem;

  @media screen and (max-width: v.$header-mobile) {
    margin-left: auto;
  }

  &:hover {
    text-decoration: underline;
  }

  &__icon {
    display: flex;
    flex-shrink: 0;
    width: 3.2rem;
    border-radius: 50%;
    background: currentColor;
    aspect-ratio: 1;
    place-items: center;
    place-content: center;

    &:before {
      display: block;
      width: 1.4rem;
      content: '';
      background: var(--c-primary);
      --mask: url(@/assets/svg/phone.svg) no-repeat center;
      -webkit-mask: var(--mask);
      mask: var(--mask);
      aspect-ratio: 1;
    }
  }

  &__text {
    @container phone (width < 20.1rem) {
      display: none;
    }
  }


}

</style>
