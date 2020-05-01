<template>
  <div>
    <div class="profil">
      <div class="main-profil">
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Profil'
}
</script>

<style scoped>
  .profil{
    position: fixed;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
    background-color: rgba(0, 0, 0, .30);
  }
  .main-profil{
    width: 400px;
    height: 450px;
    background: #fff;
    margin: 120px auto;
  }
</style>
