<script setup>
  import { ref} from 'vue';


  let isMenuOpen = ref(false);

  const toggleMenu = ()=>{
    isMenuOpen.value = !isMenuOpen.value;
  };

</script>

<template>
    <header :class="{header:true , open: isMenuOpen }">
      <div :class="{overlay: true, displayNone: !isMenuOpen, displayBlock: isMenuOpen}" @click="toggleMenu"></div>
      <nav itemscope itemtype="http://schema.org/Organization">
        <div
          class="header__logo"
          itemprop="logo"
          itemscope
          itemtype="http://schema.org/ImageObject"
        >
          <h1 itemprop="name">
            Game<span class="pacman"
              ><img src="../assets/img/Pacman.svg" alt="" /></span
            >n
            <meta itemprop="encodingFormat" content="image/svg+xml" />
          </h1>
        </div>
        <ul
          class="header__menu"
          itemscope
          itemtype="http://schema.org/MenuItem"
        >
          <li class="header__menu-item" itemprop="name">
            <a href="#" class="header__menu-link btn" itemprop="url"
              >Détail de l'évènement</a
            >
          </li>
          <li class="header__menu-item" itemprop="name">
            <a href="#" class="header__menu-link" itemprop="url">À propos</a>
          </li>
          <li class="header__menu-item" itemprop="name">
            <a href="#" class="header__menu-link" itemprop="url">Contact</a>
          </li>
          <li class="header__menu-item" itemprop="name">
            <a href="#" class="header__menu-link" itemprop="url"
              >Évènements passés</a
            >
          </li>
        </ul>

        <div class="header__toggle hide-for-xlg" @click="toggleMenu">
          <span></span>
          <span></span>
          <span></span>
        </div>
      </nav>
      <ul
        :class="{'header__menu--toggle':true, 'translateY-200': !isMenuOpen, 'translateY-0': isMenuOpen}"
        itemscope
        itemtype="http://schema.org/MenuItem"
      >
        <li class="header__menu-item" itemprop="name">
          <a href="#" class="header__menu-link btn" itemprop="url"
            >Détail de l'évènement</a
          >
        </li>
        <li class="header__menu-item" itemprop="name">
          <a href="#" class="header__menu-link" itemprop="url">À propos</a>
        </li>
        <li class="header__menu-item" itemprop="name">
          <a href="#" class="header__menu-link" itemprop="url">Contact</a>
        </li>
        <li class="header__menu-item" itemprop="name">
          <a href="#" class="header__menu-link" itemprop="url"
            >Évènements passés</a
          >
        </li>
      </ul>
    </header>
</template>