<template>
  <div class="header-container">
    <header-mobile class="desktop-hide" />
    <header-desktop class="mobile-hide" />
  </div>
</template>

<script>
import HeaderMobile from "../images/header-mobile";
import HeaderDesktop from "../images/header-desktop";

export default {
  name: "Header",
  components: {
    HeaderMobile,
    HeaderDesktop
  }
};
</script>
