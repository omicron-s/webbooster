<script setup>
import TheSection from "@/components/TheSection.vue";
import {BASE_URL} from "@/constants.js";

const glob = import.meta.glob(`@/assets/img/benefits/*.svg`,)

const benefitsList = [];

Object.entries(glob).forEach((path) => {
  const img = path[0];
  let title = 'Заголовка не нашлось';
  let text = 'Текста не нашлось';
  let i = 0;

  const icon = path[0].split('/').pop().replace('.svg', '');

  if (icon === 'quality') {
    title = 'Качественная продукция';
    text = 'Все наши товары сертифицированы и\xa0имеют сопроводительную документацию.';
    i = 0;
  }

  if (icon === 'unique') {
    title = 'Индивидуальный подход';
    text = 'Возможность изготовления компонентов специально для\xa0вас на\xa0заводах-изготовителя.';
    i = 1;
  }

  if (icon === 'free') {
    title = 'Бесплатная доставка';
    text = 'При наличии товара на складе и\xa0заказе от 10\xa0000\xa0рублей, доставим бесплатно по Москве и\xa0СПБ в\xa0течение 2х часов.';
    i = 2;
  }

  if (icon === 'similar') {
    title = 'Подбираем аналоги';
    text = 'Поможем подобрать аналоги популярных европейских брендов в\xa0условиях санкций.';
    i = 3;
  }

  if (icon === 'banked') {
    title = 'Резервный запас компонентов';
    text = 'Хранение товара на наших складах для постоянных клиентов.';
    i = 4;
  }

  if (icon === 'payment') {
    title = 'Качественная продукция';
    text = 'Отсрочка платежей для\n постоянных клиентов.';
    i = 5;
  }

  benefitsList[i] = {
    img: img,
    title: title,
    text: text
  }
})

</script>

<template>
<TheSection class="benefits">
  <template v-slot:title>Почему с нами выгодно</template>
  <template v-slot:subtitle>С 1996 года мы занимаемся оптовыми поставками электронных компонентов от ведущих
    производителей из&nbsp;Европы
    и&nbsp;Азии для&nbsp;Российских потребителей.
  </template>
  <template v-slot:content>
    <ul class="benefits__list">
      <li v-for="(item,i) in benefitsList" :key="i" class="benefits__item">
        <div :style="`--icon:url(${BASE_URL}${item.img})`" class="benefits__item-img"></div>
        <b class="benefits__item-title">{{ item.title }}</b>
        <p class="benefits__item-text">{{ item.text }}</p>
      </li>
    </ul>
  </template>
</TheSection>
</template>

<style lang="scss" scoped>
@use '@/assets/style/variables' as v;

.benefits {
  &__list {
    display: grid;
    grid-template-columns: repeat(3, minmax(26rem, 1fr));
    gap: 2rem;
    place-content: center;
    justify-items: center;

    @supports not (grid-template-rows: subgrid) {
      grid-auto-rows: 1fr;
    }


    @media screen and (max-width: v.$header-tablet) {
      grid-template-columns: repeat(auto-fit, minmax(26rem, 1fr));
    }
  }

  &__item {
    position: relative;
    display: grid;
    overflow: hidden;
    width: 100%;
    max-width: 38rem;
    padding: 4rem clamp(1.5rem, 2.4vw, 3.2rem);
    text-align: center;
    border-radius: 10px;
    background: var(--c-white);

    @supports (grid-template-rows: subgrid) {
      grid-template-rows: subgrid;
      gap: 0;
      grid-row: span 3;
    }

    @supports not (grid-template-rows: subgrid) {
      grid-auto-rows: max-content;
    }

    @media screen and (max-width: v.$header-tablet) {
      padding: 2rem 1.5rem;
    }

    &:before {
      position: absolute;
      right: -16rem;
      bottom: -30rem;
      width: 40rem;
      height: 40rem;
      content: '';
      border-radius: 30px;
      background: rgba(#5172C4, 0.07);
      rotate: 45deg;
    }

    &-img {
      font-size: 11rem;
      position: relative;
      display: flex;
      align-items: center;
      justify-content: center;
      width: 1em;
      margin: 3rem auto 7rem;
      border-radius: 50%;
      background: linear-gradient(0, #040A57, #3A23E6);
      aspect-ratio: 1;

      @media screen and (max-width: v.$header-tablet) {
        font-size: 8rem;
        margin: 2rem auto 4rem;
      }

      &:before {
        width: 50%;
        content: '';
        background: var(--c-white);
        --mask: var(--icon) no-repeat center / contain;
        -webkit-mask: var(--mask);
        mask: var(--mask);
        aspect-ratio: 1;
      }

      &:after {
        position: absolute;
        z-index: -1;
        content: '';
        border-radius: 50%;
        box-shadow: 0.064em -0.26em 0 rgba(#07086C, 0.1),
        -0.25em .12em 0 rgba(#07086C, 0.1),
        .2em 0.24em 0 rgba(#07086C, 0.1);
        inset: 0.03em;
      }
    }

    &-title {
      font-size: 2rem;
      margin-bottom: 1.4rem;
      color: #2A336C;
      @media screen and (max-width: v.$header-tablet) {
        //min-height: 2lh;
        margin-bottom: 0.5rem;
      }
    }

    &-text {
      font-size: 2rem;
      white-space: pre-line;
      color: #555;

      @media screen and (max-width: v.$header-tablet) {
        font-size: 1.8rem;
      }
    }

  }
}
</style>
