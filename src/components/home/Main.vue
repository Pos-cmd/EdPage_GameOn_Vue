<script setup>
  const emit = defineEmits(['showForm']);

  function showForm(){
    emit('showForm')
  }
</script>

<template>
    <div class="main__container" itemscope itemtype="http://schema.org/Event">
        <h2 class="main__title hide-for-lg" itemprop="name">
          Marathon national de jeux vidéos
        </h2>
        <p class="main__desc hide-for-lg" itemprop="description">
          Vous aimerez jouer ? Notre prochain évènement gaming est ouvert aux
          réservation.... Places limitées
        </p>
        <img
          src="../assets/img/gameon_700.webp"
          alt="homme jouant a un jeux"
          class="main__img hide-for-lg"
        />
        <button class="main__sub-btn btn show_form hide-for-lg" @click="showForm">
          Je M'inscris
        </button>

        <div
          class="hero main__hero"
          itemprop="subEvent"
          itemscope
          itemtype="http://schema.org/Event"
        >
          <div class="hero__container">
            <h2 class="hero__title" itemprop="name">
              Marathon national de jeux vidéos
            </h2>
            <p class="hero__desc" itemprop="description">
              Vous aimerez jouer ? Notre prochain évènement gaming est ouvert
              aux réservation.... Places limitées
            </p>
            <button
              class="hero__sub-btn btn show_form"
              itemprop="potentialAction"
              itemscope
              itemtype="http://schema.org/ReserveAction"
              @click="showForm"
            >
              Je M'inscris
            </button>
          </div>
        </div>
      </div>
</template>