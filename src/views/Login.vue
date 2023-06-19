<!-- eslint-disable vue/multi-word-component-names -->
<script setup>
import Header from "../components/Header.vue";
import { ref } from "vue";
import { useRouter } from "vue-router";
import { useStore } from "../store/index.js";
import { auth } from "../firebase/index.js";
import {
  signInWithEmailAndPassword,
  createUserWithEmailAndPassword,
  GoogleAuthProvider,
  signInWithPopup,
} from "firebase/auth";

const registerUserByGoogle = async () => {
  const provider = new GoogleAuthProvider();
  const user = await signInWithPopup(auth, provider);
  router.push("./account");
  console.log(user);
};

const store = useStore();
const router = useRouter();

const login_email = ref("");
const login_password = ref("");
const error = ref(false);

const register_email = ref("");
const register_password1 = ref("");
const register_password2 = ref("");

const login = async () => {
  try {
    await signInWithEmailAndPassword(
      auth,
      login_email.value,
      login_password.value
    );
    router.push("./account");
  } catch (error) {
    switch (error.code) {
      case "auth/user-not-found":
        alert("User not found");
        break;
      case "auth/wrong-password":
        alert("Wrong password");
        break;
      default:
        alert("Something went wrong");
    }
    return;
  }
};
const registerUser = async () => {
  if (register_password1.value !== register_password2.value) {
    alert("Please confirm your password!");
    return;
  } else {
    await createUserWithEmailAndPassword(
      auth,
      register_email.value,
      register_password1.value
    );
    router.push("./account");
  }
};
</script>

<template>
  <Header v-bind:lon="false" id="header" />
  <div class="bg">
    <div class="login-in-container">
      <div class="wrapper">
        <div class="form-box-login-in">
          <h2>Login</h2>
          <form action="#">
            <div class="input-box">
              <input
                type="email"
                required
                v-model="login_email"
                placeholder="Enter your email address."
              />
            </div>

            <div class="input-box">
              <input
                type="password"
                required
                v-model="login_password"
                placeholder="Enter your password."
              />
            </div>
          </form>

          <button id="btn_sub" @click="login()">Login</button>
        </div>
        <button id="google" @click="registerUserByGoogle()">
          Login Via Google
        </button>
      </div>
    </div>
    <div class="sign-up-container">
      <div class="wrapper">
        <div class="form-box-login-in">
          <h2>Register</h2>
          <form action="#">
            <div class="input-box">
              <input
                type="email"
                required
                v-model="register_email"
                placeholder="Enter your email address."
              />
            </div>

            <div class="input-box">
              <input
                type="password"
                required
                v-model="register_password1"
                placeholder="Enter your password."
              />
            </div>

            <div class="input-box">
              <input
                type="password"
                required
                v-model="register_password2"
                placeholder="Re-Enter your password."
              />
            </div>
          </form>

          <button id="btn_sub" @click="registerUser()">Register</button>
        </div>
        <button id="google" @click="registerUserByGoogle()">
          Register Via Google
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
#header {
  z-index: 99;
}
.login-in-container {
  border-radius: 20px;
  height: 70%;
  transform: translateY(15%);
  text-align: center;
  font-weight: 400px;
  font-size: 20px;
  color: black;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-left: 5%;
  transform: translateX(100%);
}
.sign-up-container {
  border-radius: 20px;
  width: 20%;
  height: 70%;
  transform: translateY(15%);
  margin-left: 50%;
  text-align: center;
  font-weight: 400px;
  font-size: 20px;
  color: black;
  display: flex;
  align-items: center;
  justify-content: center;
  transform: translateX(-50%);
}
.form-box-login-in {
  width: 130%;
}
input {
  width: 100%;
}
img {
  width: 35px;
  margin-left: 10px;
  transform: translateY(30%);
  background: linear-gradient(to right, black);
  border: 1px solid gray;
  border-radius: 5px;
}

div.bg {
  transform: translateY(-2%);
  width: 100%;
  height: 710px;
  background-image: url(https://kettleheroes.com/wp-content/uploads/2022/02/Why-is-Popcorn-a-Movie-Food.jpg);
  background-repeat: no-repeat;
  background-size: cover;
  display: flex;
}
button {
  width: 150px;
  height: 40px;
  margin-top: 20px;
  background: linear-gradient(to right, black);
  border: 1px solid gray;
  border-radius: 5px;
  font-family: Georgia, "Times New Roman", Times, serif;
  font-weight: 600;
  font-size: 15px;
}

#google {
  margin-left: 20%;
}

button:hover {
  color: white;
}
</style>
