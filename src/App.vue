<script setup lang="ts">
import type { Ref } from 'vue'
import { ref } from 'vue'
import Button from 'primevue/button'

const parties: Ref<Record<string, number>> = ref({
  sumar: 0,
  psoe: 0,
  pp: 0,
  vox: 0,
  nulo: 0,
  blanco: 0,
})

function add(party: string) {
  parties.value[party]++
}

function remove(party: string) {
  if (parties.value[party] > 0)
    parties.value[party]--
}

function imgImport(party: string) {
  return new URL(`./assets/images/${party}.svg`, import.meta.url).toString()
}
</script>

<template>
  <!-- <header>
    <div class="max-layout">
      <img alt="Sumar logo" class="logo" src="@/assets/images/SumarLogo.svg" width="125" height="125">
    </div>
  </header> -->
  <main>
    <section class="max-layout">
      <article v-for="(party, index) in parties" :key="`party-index-${index}-${party}`" class="party">
        <div class="party__img-cont">
          <p v-if="index === 'nulo' || index === 'blanco'" class="party__img party__count"> {{ index }}</p>
          <img v-else :alt="index" :src="imgImport(index)" class="party__img" :class="`party__img--${index}`">
        </div>
        <div class="party__input">
          <p class="party__count">
            {{ party }}
          </p>
          <div class="party__buttons">
            <Button @click="add(index)">
              <span>+</span>
            </Button>
            <Button @click="remove(index)">
              <span>-</span>
            </Button>
          </div>
        </div>
      </article>
    </section>
  </main>
</template>

<style lang="scss" src="@/style/main.scss" />
