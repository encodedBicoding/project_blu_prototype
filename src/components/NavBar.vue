<template>
  <nav class="nav_container">
    <div class="logo_container">
      <a class="logo_action" href="/">
        <img src="../assets/logo.png" width="100%" height="100%"/>
      </a>
    </div>
    <div class="logo_container">
      <a href="/" class="logo_action">
        <img src="../assets/profile.png" width="100%" height="100%"/>
      </a>
    </div>
  </nav>
</template>
<script>
export default {
  name: 'NavBar',
};
</script>
<style scoped>
.nav_container{
  position: sticky;
  top: 0;
  height: 40px;
  padding: .6rem 3rem;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  background: #000000 0% 0% no-repeat padding-box;
  opacity: 0.46;
  backdrop-filter: blur(50px);
  -webkit-backdrop-filter: blur(50px);
  z-index: 5;
}
.logo_container{
  width: auto;
  height: 70%;
}

@media screen and (max-width: 1024px) {
  .nav_container{
    padding: .7rem;
  }
  .logo_container{
  width: auto;
  height: 60%;
}
}
/* @media screen and (max-width: 850px) {}

@media screen and (max-width: 500px) {} */

</style>
