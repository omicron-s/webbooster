<script setup>
const props = defineProps({
  isExpanded: Boolean,
  navID: String
})

const emit = defineEmits(['toggleExpand'])

</script>

<template>
<button :aria-expanded="props.isExpanded" :aria-label="props.isExpanded ? 'Закрыть навигацию': 'Показать навигацию'"
        class="btn-menu" @click="emit('toggleExpand')" :aria-controls="props.navID">
  <span class="btn-menu__line _top"></span>
  <span class="btn-menu__line _middle"></span>
  <span class="btn-menu__line _bottom"></span>
</button>
</template>

<style lang="scss" scoped>
@use '@/assets/style/variables' as v;

.btn-menu {
  position: relative;
  display: none;
  align-items: center;
  justify-content: center;
  width: 3rem;
  height: 3rem;
  color: currentColor;
  background: none;
  $line-pad: 0.3rem;

  @media screen and (max-width: v.$header-mobile) {
    display: flex;
  }

  &__line {
    position: absolute;
    height: 0.4rem;
    transition: 0.05s scale, 0.05s 0.05s rotate, 0.05s 0.1s translate;
    border-radius: 4px;
    background: currentColor;

    [aria-expanded="true"] & {
      transition: 0.05s translate, 0.05s 0.05s rotate, 0.05s 0.1s scale;
    }

    &._top {
      inset: $line-pad $line-pad auto;

      [aria-expanded="true"] & {
        translate: 0 10px;
        rotate: 45deg;
        scale: 1.3 1;
      }
    }

    &._middle {
      inset: calc(50% - .2rem) $line-pad auto;

      [aria-expanded="true"] & {
        scale: 0 1;
      }
    }

    &._bottom {
      inset: auto $line-pad $line-pad;

      [aria-expanded="true"] & {
        translate: 0 -10px;
        rotate: -45deg;
        scale: 1.3 1;
        //transform: translateY(-10px) rotate(-45deg) scaleX(1.3)
      }
    }
  }

}
</style>
