<script setup>
import TheLogo from "@/components/TheLogo.vue";
import TheNav from "@/components/TheNav.vue";
import ThePhone from "@/components/ThePhone.vue";
import {onMounted, ref} from "vue";

const header = ref()
const isSticky = ref(false)

const observer = new IntersectionObserver(([e]) => isSticky.value = e.intersectionRatio < 1, {threshold: [1]})

onMounted(() => observer.observe(header.value))

const navLinks = ['Каталог', 'Производители', 'Для  кого мы работаем', 'Сертификаты', 'О нас', 'FAQ', 'Контакты']


</script>

<template>
<header ref="header" :class="{_sticky: isSticky}" class="header">
  <div class="container">
    <div class="row">
      <TheLogo />
      <TheNav :nav-links="navLinks"/>
      <ThePhone/>
    </div>
  </div>
</header>
</template>

<style lang="scss" scoped>
@use '@/assets/style/variables' as v;

.header {
  --padding-block: 0.5em;
  --header-bg: var(--c-primary);
  --shadow: drop-shadow(1px 1px 1px rgba(0, 0, 0, 0.3));
  position: sticky;
  display: flex;
  align-items: center;
  margin-top: var(--header-margin);
  color: var(--c-white);
  inset: -1px auto auto;
  padding-block: var(--padding-block);
  transition: background 0.1s ease-in-out;
  z-index: 2;

  &._sticky {
    background: var(--header-bg);
    filter: var(--shadow);
  }
}

.row {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 2rem;

  ._sticky & {
    padding-top: 1px;
  }

  @media screen and (max-width: v.$header-tablet) {
    gap: 1rem;
  }

  @media (min-width: v.$header-mobile-min) and (max-width: v.$header-tablet) {
    flex-wrap: wrap;
  }

  @media screen and (max-width: v.$header-mobile) {
    justify-content: flex-start;
  }
}
</style>
