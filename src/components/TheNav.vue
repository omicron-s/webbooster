<script setup>
import BurgerMenu from "@/components/BurgerMenu.vue";
import {ref} from "vue";

const isExpanded = ref(false)
const navID = 'header-navigation'

defineProps({
  navLinks: Array,
})

</script>

<template>
<div class="nav-wrapper">
  <BurgerMenu :isExpanded="isExpanded" :nav-i-d @toggle-expand="isExpanded = !isExpanded"/>
  <nav :id="navID" :class="{_show: isExpanded}" class="nav">
    <ul class="menu">
      <li v-for="link in navLinks" :key="link" class="menu__item">
        <a class="menu__link" href="#">{{ link }}</a>
      </li>
    </ul>
  </nav>
</div>
</template>

<style lang="scss" scoped>
@use '@/assets/style/variables' as v;

.nav-wrapper {
  flex-basis: 75rem;
  flex-grow: 1;
  flex-shrink: 1;

  @media screen and (max-width: v.$header-tablet) {
    flex-basis: 100%;
    order: 1;
  }

  @media screen and (max-width: v.$header-mobile) {
    flex-basis: 4rem;
    flex-grow: 0;
    order: -1;
  }
}

.nav {
  @media screen and (max-width: v.$header-mobile) {
    position: absolute;
    z-index: -1;
    visibility: hidden;
    overflow-y: scroll;
    transition: left 0.15s ease-in-out;
    inset: 0 auto auto -100%;

    ._sticky & {
      top: 1px;
    }

    @supports (min-height: 100svh) {
      max-height: calc(100svh - var(--header-height));
    }

    @supports not (min-height: 100svh) {
      max-height: calc(100svh - var(--header-height));
    }

    &._show {
      left: 0;
      visibility: visible;
    }
  }
}

.menu {
  display: flex;
  justify-content: space-between;
  gap: 2rem;

  @media screen and (max-width: v.$header-mobile) {
    align-items: flex-start;
    flex-direction: column;
    padding: var(--header-height) var(--container-padding) var(--padding-block);
    background: var(--header-bg);
  }

  &__item {
    flex-shrink: 0;
  }

  &__link {
    font-weight: 300;

    &:hover {
      text-decoration: underline;
    }
  }
}
</style>
