<script setup>
import TheSection from "@/components/TheSection.vue";
import TheButton from "@/components/TheButton.vue";
import {CTAFORM} from "@/constants.js";

const processList = [
  {
    title: 'Вы оставляете заявку',
    text: 'Отправить запрос вы можете любым удобным для вас способом: например, через форму на сайте. Также вы можете связаться с нами напрямую.'
  },
  {
    title: 'Мы проверяем наличие позиций',
    text: 'Проверяем наличие на складе, а также актуальность производства (возможна замена, если необходимо.) Если требуется замена - подбираем аналоги и привозим на заказ.'
  },
  {
    title: 'Формируем коммерческое предложение',
    text: 'На данном этапе мы с вами согласуем ценовое предложение, обговариваем сроки поставки и условия оплаты.'
  },
  {
    title: 'Проводим оплату',
    text: 'Далее, после получения авансового платежа, мы размещаем заказ.'
  },
  {
    title: 'Мы выполняем заказ',
    text: 'Товар поступает на склад в Москву или Санкт-Петербург, где мы сверяем правильность поставки и начинаем сборку.'
  },
  {
    title: 'Вы получаете товар',
    text: 'Поставляем вам товар в надлежащей упаковке в сопровождении оригиналов всех необходимых документов либо вы забираете его самовывозом.'
  },
]
</script>

<template>
<TheSection class="process">
  <template v-slot:title>Схема работы</template>
  <template v-slot:subtitle>Lorem ipsum dolor sit amet consectetur. Augue velit in enim sagittis imperdiet sit mauris.
    Vitae sit in fusce massa amet.
  </template>
  <template v-slot:content>
    <ol class="process__list">
      <li v-for="(item, i) in processList" :key="i" class="process__item">
        <b aria-hidden="true" class="process__item-number">{{ (i + 1).toString().padStart(2, '0') }}</b>
        <strong class="process__item-title">{{ item.title }}</strong>
        <p class="process__item-desc">{{ item.text }}</p>
      </li>
    </ol>
    <TheButton :href="`#${CTAFORM}`" class="process__cta">
      Оставить заявку
    </TheButton>
  </template>
</TheSection>
</template>

<style lang="scss" scoped>
@use '@/assets/style/variables' as v;

.process {
  margin-top: -5rem;
  padding-top: calc(var(--padding-top) + 5rem);


  @media screen and (min-width: v.$header-mobile-min) {
    background: url(@/assets/img/process/bg.png) no-repeat center / cover;
  }

  &__list {
    display: grid;
    margin-bottom: 4rem;
    grid-template-columns: repeat(3, minmax(1rem, 1fr));
    gap: 1.5rem;

    @media screen and (max-width: v.$header-tablet) {
      grid-template-columns: repeat(2, minmax(1rem, 1fr));
    }

    @media screen and (max-width: v.$header-sm) {
      grid-template-columns: 1fr;
    }
  }

  &__item {
    position: relative;
    z-index: 0;
    display: grid;
    align-items: center;
    min-height: 27rem;
    padding: 4rem 2.5rem 2rem 4rem;
    color: var(--c-white);
    border-radius: 20px;
    background: linear-gradient(90deg, #041080, #0926C0);
    grid-template-columns: auto 1fr;
    gap: 2.8rem 1.6rem;

    @supports (grid-template-rows: subgrid) {
      grid-template-rows: subgrid;
      grid-row: span 2;
    }

    @media screen and (max-width: v.$header-tablet) {
      padding: 3rem 2rem 2rem 3rem;
      gap: 2rem 1.6rem;
    }

    @media screen and (max-width: v.$header-sm) {
      &:not(:first-child) {
        clip-path: polygon(calc(50% + 2px) 28px, calc(50% + 33px) 0, 100% 0, 100% calc(100% + 41px), -41px calc(100% + 41px), -41px 0, calc(50% - 29px) 0);
      }
    }

    &:not(:last-child)::before {
      position: absolute;
      z-index: -1;
      content: '';
      background: #0926C0;
      -webkit-mask: var(--mask);
      mask: var(--mask);
      inset: 0 -25px 0 calc(100% - 1px);
      --mask: url(@/assets/img/process/item1.svg) no-repeat center right;


      @media screen and (max-width: v.$header-sm) {
        background: linear-gradient(90deg, #041080, #0926C0);
        inset: calc(100% - 1px) 0 -26px 0;
        --mask: url(@/assets/img/process/item2.svg) no-repeat center bottom;
        scale: 1;
      }
    }


    &:nth-child(2) {
      @media screen and (min-width: v.$header-tablet-min) {
        clip-path: polygon(0 calc(50% - 41px), 0 0, calc(100% + 41px) 0, calc(100% + 41px) 100%, 0 100%, 0 calc(50% + 41px), 26px 50%);
      }

      @media (min-width: v.$header-sm-min) and (max-width: v.$header-tablet) {
        clip-path: polygon(0 calc(50% - 41px), 0 0, 100% 0, 100% calc(100% + 41px), 0 calc(100% + 41px), 0 calc(50% + 41px), 26px 50%);

        &:before {
          background: linear-gradient(90deg, #041080, #0926C0);
          inset: calc(100% - 1px) 0 -26px 0;
          --mask: url(@/assets/img/process/item2.svg) no-repeat center bottom;
        }
      }
    }

    &:nth-child(3) {
      @media screen and (min-width: v.$header-tablet-min) {
        clip-path: polygon(0 calc(50% - 41px), 0 0, 100% 0, 100% calc(100% + 41px), 0 calc(100% + 41px), 0 calc(50% + 41px), 26px 50%);

        &:before {
          background: linear-gradient(90deg, #041080, #0926C0);
          inset: calc(100% - 1px) 0 -26px 0;
          --mask: url(@/assets/img/process/item2.svg) no-repeat center bottom;
        }
      }

      @media (min-width: v.$header-sm-min) and (max-width: v.$header-tablet) {
        order: 2;
        clip-path: polygon(calc(50% + 2px) 28px, calc(50% + 33px) 0, 100% 0, 100% 100%, -41px 100%, -41px 0, calc(50% - 29px) 0);

        &:before {
          background: #041080;
          --mask: url(@/assets/img/process/item1.svg) no-repeat center right;
          inset: 0 calc(100% - 1px) 0 -26px;
          scale: -1;
        }
      }
    }

    &:nth-child(4) {
      @media screen and (min-width: v.$header-tablet-min) {
        order: 2;
        clip-path: polygon(calc(50% + 2px) 28px, calc(50% + 33px) 0, 100% 0, 100% 100%, -41px 100%, -41px 0, calc(50% - 29px) 0);

        &:before {
          background: #041080;
          inset: 0 calc(100% - 1px) 0 -26px;
          scale: -1;
        }
      }

      @media (min-width: v.$header-sm-min) and (max-width: v.$header-tablet) {
        order: 1;
        clip-path: polygon(100% calc(50% - 41px), calc(100% - 26px) 50%, 100% calc(50% + 41px), 100% calc(100% + 41px), -41px calc(100% + 41px), -41px 0, 100% 0);

        &:before {
          background: linear-gradient(90deg, #041080, #0926C0);
          inset: calc(100% - 1px) 0 -26px 0;
          --mask: url(@/assets/img/process/item2.svg) no-repeat center bottom;
          scale: 1;
        }
      }
    }

    &:nth-child(5) {
      @media screen and (min-width: v.$header-tablet-min) {
        order: 1;
        clip-path: polygon(100% calc(50% - 41px), calc(100% - 26px) 50%, 100% calc(50% + 41px), 100% 100%, -41px 100%, -41px 0, 100% 0);

        &:before {
          background: #041080;
          inset: 0 calc(100% - 1px) 0 -26px;
          scale: -1;
        }
      }

      @media (min-width: v.$header-sm-min) and (max-width: v.$header-tablet) {
        order: 3;
        clip-path: polygon(calc(50% + 2px) 28px, calc(50% + 33px) 0, calc(100% + 41px) 0, calc(100% + 41px) 100%, -41px 100%, -41px 0, calc(50% - 29px) 0);

        &:before {
          background: #0926C0;
          inset: 0 -25px 0 calc(100% - 1px);
          --mask: url(@/assets/img/process/item1.svg) no-repeat center right;
          scale: 1;
        }
      }
    }

    &:nth-child(6) {
      @media screen and (min-width: v.$header-tablet-min) {
        clip-path: polygon(100% calc(50% - 41px), calc(100% - 26px) 50%, 100% calc(50% + 41px), 100% 100%, -41px 100%, -41px 0, 100% 0);
      }

      @media (min-width: v.$header-sm-min) and (max-width: v.$header-tablet) {
        order: 4;
        clip-path: polygon(0 calc(50% - 41px), 0 0, calc(100% + 41px) 0, calc(100% + 41px) 100%, 0 100%, 0 calc(50% + 41px), 26px 50%);
      }

    }

    &-number {
      font-size: 3.6rem;
      font-weight: 900;
      color: var(--c-additional);
      @media screen and (max-width: v.$header-tablet) {
        font-size: 3rem;
      }
    }

    &-title {
      font-weight: 900;
      display: flex;
      align-items: center;
      text-transform: uppercase;
    }

    &-desc {
      align-self: start;
      grid-column: 2;
      @media screen and (max-width: 1040px) {
        grid-column: span 2;
      }
    }
  }

  &__cta {
    margin-inline: auto;
  }
}

</style>
