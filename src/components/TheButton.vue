<script setup>
import {computed, ref} from "vue";

const isHover = ref(false)

const props = defineProps({
  href: String
})

const tag = computed(() => props.href ? 'a' : 'button')
</script>

<template>
<component :is="tag" :href="props.href" class="button" @mouseleave="isHover = false" @mouseover="isHover = true">
  <slot v-if="!isHover"></slot>
  <span v-else class="wtf">Почему в макете кривой текст? xD</span>
</component>
</template>

<style lang="scss" scoped>
.button {
  font-size: 1.8rem;
  max-width: 30rem;
  min-height: var(--interactive-height);
  text-transform: uppercase;
  color: var(--c-white);
  border-radius: 10px;
  background: #FFA500;
  display: flex;
  text-align: center;
  align-items: center;
  justify-content: center;
  padding-inline: 0.5rem;

  &:hover {
    opacity: 0.8;
  }

  &:active {
    opacity: 0.6;
  }

  .wtf {
    font-size: 1.6rem;
    text-transform: none;
  }
}
</style>
