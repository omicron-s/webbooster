<script setup>
import TheCTA from "@/components/TheCTA.vue";

const benefitsList = ['Отсрочка платежей для постоянных клиентов', 'Бесплатная доставка по Москве и СПБ в течение 2х часов', 'Квалифицированный персональный менеджер']
</script>

<template>
<section aria-label="Semitex" class="heading">
  <div class="container">
    <div class="heading__grid">
      <div class="heading__block">
        <h1 class="heading__title">Оптовые поставки <span class="heading__title-small">электронных компонентов</span>
          <span
              class="heading__title-medium">из Китая день в день</span></h1>
        <p class="heading__subtitle">
          Комплексные поставки электронных компонентов и оборудования. <br>Подберем аналоги популярных брендов из Европы
          в
          условиях санкций.
        </p>
        <ul class="heading__benefits">
          <li v-for="item in benefitsList" :key="item">{{ item }}</li>
        </ul>
      </div>
      <TheCTA/>
    </div>
  </div>
</section>

</template>

<style lang="scss" scoped>
@use '@/assets/style/variables' as v;

.heading {
  min-height: 85rem;
  margin-top: calc((var(--header-height) + var(--header-margin)) * -1);
  padding-top: 18rem;
  padding-bottom: 6rem;
  background: var(--c-primary);

  @media screen and (max-width: v.$header-tablet) {
    min-height: 60rem;
    padding-top: 14rem;
  }

  @media screen and (max-width: v.$header-mobile) {
    padding-top: 8rem;
  }

  @media screen and (min-width: v.$header-mobile-min) {
    background: url(@/assets/img/heading/bg2.png) no-repeat center/cover, var(--c-primary);
    --mask: url(@/assets/img/heading/bg1.svg) no-repeat center/ clamp(120rem, 100vw, 100%) 100%;
    -webkit-mask: var(--mask);
    mask: var(--mask);
  }

  &__grid {
    display: grid;
    gap: 3rem;

    @media screen and (min-width: v.$header-mobile-min) {
      grid-template-columns: minmax(40rem, 80rem) minmax(26rem, 38rem);
      grid-auto-flow: column;
      place-content: space-between;
    }
  }

  &__block {
    color: var(--c-white);
    container-type: inline-size;

    @media screen and (max-width: v.$header-mobile) {
      text-align: center;
    }
  }

  &__title {
    font-size: clamp(3rem, 8.5cqw, 6.8rem);
    font-weight: 900;
    line-height: 1;
    margin-bottom: 0.5rem;
    text-transform: uppercase;

    &-small {
      font-size: clamp(3rem, 7cqw, 5.6rem);
      display: block;
      text-transform: lowercase;
      color: var(--c-additional);
    }

    &-medium {
      font-size: clamp(3rem, 7.6cqw, 6rem);
      line-height: 1.3;
    }

  }

  &__subtitle {
    font-size: clamp(1.8rem, 3cqw, 2.4rem);
    margin-bottom: 3.5rem;
    color: var(--c-additional);
  }

  &__benefits {
    font-size: clamp(1.8rem, 2.8cqw, 2.2rem);
    padding: 2.5rem 3rem;
    text-align: left;
    border-radius: 10px;
    background: linear-gradient(0.25turn, rgb(from var(--c-additional) r g b / 0.3), transparent);

    > li {
      display: flex;

      &::before {
        flex-shrink: 0;
        width: 2rem;
        height: 2rem;
        margin-top: 0.4rem;
        margin-right: 1.4rem;
        content: '';
        background: linear-gradient(0.25turn, #48FFFF, 96%, #25A4F1);
        --mask: url(@/assets/svg/check.svg) no-repeat center/1.4rem 1.1rem;
        -webkit-mask: var(--mask);
        mask: var(--mask);
      }
    }

    @media screen and (max-width: v.$header-tablet) {
      padding: 1rem;
    }
  }
}
</style>
