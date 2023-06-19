<!-- eslint-disable vue/multi-word-component-names -->
<script setup>
</script>

<template>
  <div class="hero-container">
    <h1 class="content">
    PopCorn Movies Office Website
    </h1>
    <p class="content">
    Movies Changes your live, explore Now.
    </p>
  </div>
</template>

<style scoped>
.hero-container {
  margin-top: 5%;
  position:relative;
  width:100%;
  height:75%;
  font-size: 1.5rem;
}

.hero-container::before {
  content: "";
  top: 0px;
  right: 0px;
  bottom: 0px;
  left: 0px;
  opacity: 0.75;
  background-image:url(https://onlyoneagleway.com/wp-content/uploads/2018/04/Alternate-Content-Picture-900x598.jpg);
  background-size:cover;
  position: absolute;
  height: 100%;
}

.content{
  font-family:'Times New Roman', Times, serif;
  position:relative;
}
</style>