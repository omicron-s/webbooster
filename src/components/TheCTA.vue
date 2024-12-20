<script setup>

import CTAForm from "@/components/CTAForm.vue";
import {CTAFORM} from "@/constants.js";
</script>

<template>
<section aria-label="Закажите обратный звонок" class="cta" :id="CTAFORM">
  <div class="cta__title">
    Закажите <br>обратный звонок
  </div>
  <CTAForm/>
</section>
</template>

<style lang="scss" scoped>
@use '@/assets/style/variables' as v;
.cta {
  display: grid;
  border-radius: 10px;
  contain: paint;
  grid-template-rows: auto 1fr;

  &__title {
    font-size: 2.3rem;
    font-weight: 900;
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 11rem;
    padding: 1rem 2rem;
    text-align: center;
    text-transform: uppercase;
    color: var(--c-white);
    background: linear-gradient(0, #6A32B4, #552693);
    @media screen and (max-width: v.$header-mobile) {
      min-height: 8rem;
    }
  }
}
</style>
