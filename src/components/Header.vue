<!-- eslint-disable vue/multi-word-component-names -->
<script setup>
import { useRouter } from "vue-router";
import { auth } from "../firebase/index.js";
import { signOut } from "firebase/auth";

const router = useRouter();

const moveLogin = () => {
  router.push("./login");
};

const moveCart = () => {
  router.push("./cart");
};

const moveIndex = () => {
  router.push("./");
};

const moveHome = () => {
  router.push("./account");
};

const logout = async () => {
  await signOut(auth);
  router.push("/login");
};

// eslint-disable-next-line no-unused-vars
const props = defineProps({
  lon: Boolean,
});
</script>

<template>
  <div class="grid-container">
    <div class="item">
      <p id="logo" @click="moveIndex">PopCorn Movies</p>
    </div>
    <div class="grid-item">
      <p v-if="!lon" />
      <button id="logout" @click="logout" v-if="lon">Log Out</button>
    </div>
    <div class="grid-item">
      <button id="home" @click="moveHome" v-if="lon">Home</button>
    </div>
    <div class="grid-item">
      <button id="login" @click="moveLogin" v-if="!lon">Login</button>

      <button id="cart" @click="moveCart" v-if="lon">Cart</button>
    </div>
  </div>
</template>

<style scoped>
.grid-container {
  position: absolute;
  display: grid;
  grid-template-columns: 2fr 2fr 2fr 2fr;
  width: 100vw;
  height: 15%;
  color: black;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  background-color: blanchedalmond;
  font-size: 3rem;
  margin-top: 0;
  padding-top: 0;
  top: 5px;
}

#logout {
  width: 200px;
}

#logo {
  margin-top: 5%;
  padding-top: 0;
  padding-left: 20px;
  height: 40px;
  width: auto;
}

.grid-item {
  background-color: blanchedalmond;
  font-size: 30px;
  text-align: center;
  height: 50px;
  width: auto;
  margin-top: 8%;
  margin-left: 100px;
}
button {
  border: 0;
  background: 0;
  font-size: 2vw;
  font-weight: bold;
}
button:hover {
  color: lightblue;
}
.item {
  width: 150%;
}
</style>
