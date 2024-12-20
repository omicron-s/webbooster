<script setup>

</script>

<template>
<section class="section">
  <div class="container">
    <div class="section__header">
      <h2 class="section__title">
        <slot name="title"></slot>
      </h2>
      <p v-if="$slots.subtitle" class="section__subtitle">
        <slot name="subtitle"></slot>
      </p>
    </div>
    <div class="section__content">
      <slot name="content"></slot>
    </div>
  </div>
</section>
</template>

<style lang="scss" scoped>
@use '@/assets/style/variables' as v;

.section {
  --padding-top: 8.5rem;
  padding-block: var(--padding-top) 13rem;

  @media screen and (max-width: v.$header-tablet) {
    padding-bottom: 8rem;
    --padding-top: 6rem;
  }

  @media screen and (max-width: v.$header-mobile) {
    padding-bottom: 6rem;
    --padding-top: 4rem;
  }

  &._inverse {
    color: var(--c-white);
  }

  &__header {
    display: grid;
    max-width: 106rem;
    margin-bottom: 4.5rem;
    text-align: center;
    margin-inline: auto;
    container-type: inline-size;
    gap: 2.5rem;
  }

  &__title {
    font-size: clamp(3rem, 5cqw, 4.5rem);
    font-weight: 900;
    line-height: 1;
    text-wrap: balance;

    &:not(._inverse) & {
      color: #111;
    }
  }

  &__subtitle {
    font-size: clamp(1.8rem, 3cqw, 2.2rem);
    line-height: 1.2;

    &:not(._inverse) & {
      color: var(--c-dark);
    }
  }
}
</style>
