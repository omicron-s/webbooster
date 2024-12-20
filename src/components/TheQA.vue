<script setup>
import TheSection from "@/components/TheSection.vue";
import {onMounted, ref} from "vue";

const list = {
  question: 'Lorem ipsum dolor sit amet consectetur. Ultrices aliquam.',
  answer: '<p>Like the phrase “stem cell” itself, “stem cell therapy” is often used to describe a variety of different medical therapies that utilize stem cells in some form to treat a patient. Sometimes the term is used incorrectly to refer to platelet rich plasma (PRP) injections. The term is also used to refer to stem cell transplants, also known as bone marrow transplants.</p><p>Most commonly “stem cell therapy” is used to describe a procedure where the patient’s adult stem cells and other potentially regenerative cells are harvested from a tissue sample of either fat or bone marrow taken from the patient. These concentrated regenerative cells are then used to treat specific injuries typically by injecting them into the afflicted area. It should be said that this type of stem cell therapy is currently not FDA approved and clinics performing it illegally in the US or in other countries perform various versions of the procedure to treat illnesses and injuries with little to no clinical evidence.</p><p>At InGeneron we use the term “regenerative cell therapy” since there are many different cell types and regenerative properties collected and used by our therapy along with adult stem cells. Importantly we do not treat patients outside of our approved clinical trials and we are dedicated to securing FDA approval through rigorous clinical testing.</p>'
}

const isAnimated = ref(false)

const detailsRef = ref()
let detailsArray = { detailsRef }

onMounted(() => {
  detailsArray = detailsRef.value.map(item => item.querySelector('.details') )
})

function toggleDetails(e) {
  const summary = (target) => target.firstElementChild;
  const details = e.target.closest('.details');

  if (!details.open && !isAnimated.value) {
    openDetails()
  }

  if (details.open && !isAnimated.value) {
    closeDetails()
  }

  function openDetails() {
    details.open = true;
    const animation = changeHeight(details, false)

    animation.onfinish = endAnimate;
    closeAllInactiveDetails()
  }

  function closeDetails() {
    const animation = changeHeight(details)

    animation.onfinish = () => {
      endAnimate();
      details.open = false
    };
  }

  function closeAllInactiveDetails (){
    detailsArray.forEach((item) => {
      if(item !== details) {
        const animation = changeHeight(item)
        animation.onfinish = () => item.open = false;
      }
    })
  }

  function changeHeight(target, toShrink = true) {
    const fullHeight = `${target.offsetHeight}px`;
    const minHeight = `${summary(target).clientHeight}px`;
    isAnimated.value = true;

    return target.animate({
      height: toShrink ? [fullHeight, minHeight] : [minHeight, fullHeight]
    }, {
      duration: 200,
      easing: 'ease-out'
    });
  }

  function endAnimate() {
    isAnimated.value = false;

    if (window.innerWidth <= 940) {
      summary(details).scrollIntoView({behavior: "smooth", block: "center"});
    }
  }

}

</script>

<template>
<TheSection class="qa _inverse">
  <template #title>Ответы на самые популярные вопросы в сфере
  </template>
  <template #content>
    <ul class="qa__list">
      <li v-for="i in 5" :key="i" :ref="detailsArray.detailsRef">
        <details :class="{_animate: isAnimated}" class="details" @click.prevent="toggleDetails">
          <summary ref="summaryRef" class="details__title">
            {{ list.question }}
            <span class="details__title-icon"></span></summary>
          <div class="details__text" v-html="list.answer">
          </div>
        </details>
      </li>
    </ul>
  </template>
</TheSection>
</template>

<style lang="scss" scoped>
@use '@/assets/style/variables' as v;

@property --bg-title-c-1 {
  syntax: '<color>';
  inherits: true;
  initial-value: #fff;
}

@property --bg-title-c-2 {
  syntax: '<color>';
  inherits: true;
  initial-value: #BDC0FF;
}

.qa {
  background: linear-gradient(0, #041080, #0926C0);

  @media screen and (min-width: v.$header-mobile-min) {
    margin-top: -5rem;
    background: url(@/assets/img/qa/bg2.png) no-repeat center/cover, linear-gradient(90deg, #041080, #0926C0);
    --mask: url(@/assets/img/qa/bg1.svg) no-repeat center/ clamp(120rem, 100vw, 100%) 100%;
    -webkit-mask: var(--mask);
    mask: var(--mask);
  }


  &__list {
    display: grid;
    gap: 1.2rem;
  }
}

.details {
  border-radius: 10px;
  background: var(--c-white);
  --bg-title-c-1: var(--c-white);
  --bg-title-c-2: #BDC0FF;
  --padding-inline: 4rem 5rem;


  &._animate {
    overflow: hidden;
  }

  &__title {
    font-size: 2.4rem;
    font-weight: 600;
    display: flex;
    padding: 2.4rem 3.5rem 2.4rem 5rem;
    transition: --bg-title-c-1 0.1s ease-in-out, --bg-title-c-2 0.1s ease-in-out, color 0.1s ease-in-out;
    color: #333;
    border-radius: 10px;
    background: linear-gradient(180deg, var(--bg-title-c-1), var(--bg-title-c-2));
    gap: 1rem;

    [open] & {
      color: var(--c-white);
      --bg-title-c-1: #969AF7;
      --bg-title-c-2: #686EEC;
    }

    @media screen and (max-width: v.$header-mobile) {
      font-size: 1.8rem;
      padding: 2rem 1rem;
    }

    &-icon {
      display: flex;
      align-items: center;
      flex-shrink: 0;
      justify-content: center;
      width: 4rem;
      height: 4rem;
      margin-left: auto;
      transition: 0.1s ease-in-out;
      color: var(--c-white);
      border-radius: 50%;
      background: #757AEF;

      @media screen and (max-width: v.$header-mobile) {
        width: 3rem;
        height: 3rem;
      }

      [open] & {
        color: #000985;
        background: var(--c-white);
      }

      &:before {
        width: 1.1rem;
        height: 1.4rem;
        content: '';
        background: currentColor;
        --mask: url(@/assets/svg/chevron.svg) no-repeat center / contain;
        -webkit-mask: var(--mask);
        mask: var(--mask);
        rotate: -90deg;

        @media screen and (max-width: v.$header-mobile) {
          scale: 0.9;
        }

        [open] & {
          rotate: 90deg;
        }

      }
    }
  }

  &__text {
    padding: 4rem 4rem 4.5rem 5rem;
    color: var(--c-dark);

    @media screen and (max-width: v.$header-mobile) {
      padding: 2rem 1rem;
    }
  }
}

</style>
