<script setup>
import TheLogo from "@/components/TheLogo.vue";
import TheButton from "@/components/TheButton.vue";
import {CTAFORM} from "@/constants.js";

const navLinks = ['Каталог', 'Производители', 'Для  кого мы работаем', 'Сертификаты', 'О нас', 'Контакты']
</script>

<template>
<footer class="footer">
  <div class="container">
    <div class="row">
      <TheLogo/>
      <nav class="nav">
        <ul class="menu">
          <li v-for="link in navLinks" :key="link" class="menu__item">
            <a class="menu__link" href="#">{{ link }}</a>
          </li>
        </ul>
      </nav>
      <TheButton :href="`#${CTAFORM}`" class="footer__cta">
        Оставить заявку
      </TheButton>
    </div>
    <div class="footer__wrong">Зачем в футере дубликат шапки, если она фиксированная? xD</div>
  </div>
</footer>
</template>

<style lang="scss" scoped>
@use '@/assets/style/variables' as v;
.footer {
  color: var(--c-white);
  background: #333333;
  padding-block: 6rem;

  @media screen and (max-width: v.$header-tablet) {
    padding-block: 3rem;
  }

  &__cta {
    flex: 2;
    min-width: 18rem;
  }

  &__wrong {
    text-align: center;
    margin-top: 1rem;
    @media screen and (min-width: v.$header-tablet-min) {
      display: none;
    }
  }
}

.row {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 2rem;

  @media screen and (max-width: v.$header-tablet) {
    //display: grid;
  }
}

.nav {
  flex-basis: 65rem;
  flex-grow: 1;
  container: footer-menu / inline-size;

  @media screen and (max-width: v.$header-tablet) {
    display: none;
  }
}

.menu {
  display: grid;
  grid-auto-flow: column;
  gap: 2rem;

  @container footer-menu (width < 68rem) {
    grid-template-columns: repeat(3, 1fr);
    grid-auto-flow: dense;
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
