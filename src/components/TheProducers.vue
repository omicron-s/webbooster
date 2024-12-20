<script setup>
import TheSection from "@/components/TheSection.vue";
import {ref} from "vue";
import {Swiper, SwiperSlide} from "swiper/vue";
import {Autoplay, Keyboard} from "swiper/modules";
import 'swiper/css';
import 'swiper/css/autoplay';
import 'swiper/css/keyboard';

const modules = [Keyboard, Autoplay]

const wrongButtons = ref(false);

const glob = import.meta.glob(['@/assets/img/producers/*.{jpg,png,webp}', '!@/assets/img/producers/bg*.{jpg,png,webp}'], {eager: true})
const sponsorList = Object.entries(glob).map(path => ({src: path[0], title: path[0].split('/').pop().split(".")[0]}));

const swiperInstance = ref()
const onSwiper = (swiper) => swiperInstance.value = swiper
const slidePrev = () => swiperInstance.value.slidePrev()
const slideNext = () => swiperInstance.value.slideNext()
</script>

<template>
<TheSection class="producers _inverse">
  <template v-slot:title>Наши производители</template>
  <template v-slot:content>
    <div class="swiper__wrapper" @mouseleave="wrongButtons = false" @mouseover="wrongButtons = true">
      <button class="swiper__button" @click="slidePrev" aria-label="Свайпнуть назад"></button>
      <swiper :autoplay="{delay: 2500, disableOnInteraction: false,}"
              :keyboard="{enabled: true }"
              :loop="true"
              :modules="modules"
              :slides-per-view="'auto'"
              :space-between="20"
              class="swiper"
              @swiper="onSwiper">
        <swiper-slide v-for="(item,i) in sponsorList" :key="i" class="swiper__slide">
          <img :alt="`Производитель: ${item.title}`" :src="item.src">
        </swiper-slide>
      </swiper>
      <button class="swiper__button _next" @click="slideNext" aria-label="Свайпнуть вперед"></button>
    </div>
    <p :class="{_wrong: wrongButtons}" class="producers__text">Lorem ipsum dolor sit amet consectetur. Non eget blandit
      in euismod felis id quisque nunc. Non orci lacus elit mauris velit gravida imperdiet id. Ipsum pulvinar ac ut
      sociis. Sed magna gravida consequat et euismod aenean quis mauris. Ut etiam egestas ultrices faucibus ultrices
      nisl enim consequat faucibus. Nibh id leo ullamcorper eleifend. Id at commodo interdum et leo.</p>
  </template>
</TheSection>
</template>

<style lang="scss" scoped>
@use '@/assets/style/variables' as v;

.producers {
  background: #0809A7;

  @media screen and (min-width: v.$header-mobile-min) {
    background: url(@/assets/img/producers/bg2.webp) no-repeat center/cover, #0809A7;
    --mask: url(@/assets/img/producers/bg1.svg) no-repeat center/ clamp(120rem, 100vw, 100%) 100%;
    -webkit-mask: var(--mask);
    mask: var(--mask);
  }

  &__text {
    position: relative;

    &._wrong {
      transition: 0.1s ease-in-out;
      color: transparent;

      &:before {
        opacity: 1;
      }
    }

    &:before {
      font-weight: 900;
      position: absolute;
      content: 'Кнопки свайпера не в контейнере... это плохо...';
      transition: 0.1s ease-in-out;
      opacity: 0;
      color: var(--c-white);
    }
  }
}

.swiper {
  max-width: 100%;
  gap: 2rem;


  &__wrapper {
    display: flex;
    justify-content: space-between;
    margin-bottom: 4rem;
    gap: 2rem;
    place-items: center;
  }

  &__slide {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 17rem;
    padding: .5rem;
    border-radius: 10px;
    background: var(--c-white);
    max-width: 24rem;
  }

  &__button {
    border-radius: 50%;
    width: 4rem;
    height: 4rem;
    background: rgb(from var(--c-white) r g b / 0.5);
    transition: background 0.2s ease-in-out;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;

    @media screen and (max-width: v.$header-mobile) {
      display: none;
    }

    &:hover {
      background: rgb(from var(--c-white) r g b / 0.7);
    }

    &:active::before {
      scale: 1.5;
    }

    &:before{
      content: '';
      --mask: url(@/assets/svg/chevron.svg) no-repeat center / contain;
      background: var(--c-white);
      -webkit-mask: var(--mask);
      mask: var(--mask);
      width: 1.1rem;
      height: 1.3rem;
      transition: 0.1s ease-in-out;
      padding-left: 0.3rem;
    }

    &._next:before {
      rotate: 180deg;
    }
  }
}

</style>
