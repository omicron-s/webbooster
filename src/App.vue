<script setup>
import TheHeading from "@/components/TheHeading.vue";
import TheHeader from "@/components/TheHeader.vue";
import TheBenefits from "@/components/TheBenefits.vue";
import TheProducers from "@/components/TheProducers.vue";
import TheProcess from "@/components/TheProcess.vue";
import TheQA from "@/components/TheQA.vue";
import TheFooter from "@/components/TheFooter.vue";
</script>

<template>
<TheHeader/>
<TheHeading/>
<TheBenefits/>
<TheProducers/>
<TheProcess/>
<TheQA />
<TheFooter/>
</template>

<style lang="scss">
@use '@/assets/style/variables' as v;

body {
  --header-height: 5.6rem;
  --header-margin: 5.6rem;
  --interactive-height: 5.6rem;

  @media (min-width: v.$header-mobile-min) and (max-width: v.$header-tablet) {
    --header-height: 9rem;
  }

  @media screen and (max-width: v.$header-tablet) {
    --header-margin: 0px;
    --interactive-height: 4rem;
  }

}
</style>
