<template>
  <div class="app-header">
    <div class="app-header__logo"><a href="/">CineStar Zagreb</a></div><!-- /.logo -->

    <ul class="app-header__navigation navigation">
      <li class="navigation__item">Pregled predstava</li><!-- /.navigation__item -->
      <li class="navigation__item navigation__item--selected">Odaberite sjedala</li><!-- /.navigation__item -->
      <li class="navigation__item">Košarica</li><!-- /.navigation__item -->
      <li class="navigation__item">Plaćanje</li><!-- /.navigation__item -->
      <li class="navigation__item">Potvrda</li><!-- /.navigation__item -->
    </ul><!-- /.app-header__navigation -->
  </div><!-- /.app-header -->
</template>

<script>
export default {
  name: 'app-header'
}
</script>

<style lang="scss">
.app-header {
  align-items: flex-start;
  border-bottom: 2px solid rgba(255,255,255,0.2);
  display: flex;
  flex-direction: row;
  height: 80px;
  justify-content: flex-start;

  &__logo {
    display: flex;
    font-weight: 700;
    line-height: 80px;
    margin-right: 128px;

    a {
      color: #fff;
      text-decoration: none;
    }
  }

  &__navigation {
    display: flex;
    flex-direction: row;
    list-style-type: none;
  

    .navigation {
      &__item {
        cursor: pointer;
        display: flex;
        flex-direction: column;
        line-height: 80px;
        margin-right: 40px;

        &:hover {
          color: #fb024e;
        }

        &--selected {
          color: #fb024e;
          font-weight: 900;
        }
      }
    }
  }
}
</style>
