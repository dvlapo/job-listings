<template>
  <header class="header"></header>
</template>

<script>
export default {};
</script>

<style>
.header {
  background-image: url('./assets/bg-header-desktop.svg');
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
  background-color: hsl(180, 29%, 50%);
  min-height: 15vh;
  margin-bottom: clamp(3rem, 5vh, 10rem);
}
@media (max-width: 420px) {
  .header {
    background-image: url('./assets/bg-header-mobile.svg');
  }
}
</style>
