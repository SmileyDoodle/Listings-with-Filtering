<template>
  <header id="header">
      <img alt="bg" src="../assets/images/bg-header-desktop.svg" class="desktopImage">
      <img alt="bg" src="../assets/images/bg-header-mobile.svg" class="mobileImage">
  </header>
</template>

<script>
export default {
    name: 'Header'
}
</script>

<style>
#header {
    background-color: hsl(180, 29%, 50%);
    height: 166px;
}
#header img {
    width: 100%;
    height: 100%;
}
.mobileImage {
    display: none;
}


@media screen and (max-width: 600px) {
  #header {
    height: 130px;
  }
  .desktopImage {
      display: none;
  }
  .mobileImage {
    display: block;
    height: 130px;
}
}
</style>