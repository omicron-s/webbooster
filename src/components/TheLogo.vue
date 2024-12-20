<script setup>

</script>

<template>
<a class="logo" href="/">
  <img alt="Semitex" src="@/assets/img/logo.png">
</a>
</template>

<style lang="scss" scoped>
@use '@/assets/style/variables' as v;

.logo {
  flex-shrink: 0;
  display: flex;
  align-items: center;
  padding: 0.2rem;
  align-self: stretch;

  &:hover {
    opacity: 0.7;
  }

  @media screen and (max-width: v.$header-tablet) {
    width: 10rem;
  }
}

</style>
