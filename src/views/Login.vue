<template>
  <div class="container">
    <h2><u>Add HR Staff</u></h2>
    <div class="form">
      <form @submit.prevent="onLogin" action="#" class="login-form">
        <input
          v-model="form.email"
          type="text"
          name="username"
          placeholder="Email"
        />
        <input
          v-model="form.password"
          type="password"
          name="password"
          placeholder="Password"
        />
        <button class="btn">Login</button>
      </form>
      <p v-if="isLoginValid">LoggedIn</p>
      <p v-else>Not LoggedIn</p>
      <p v-for="user in users" v-bind:key="user">{{ user }}</p>
    </div>
  </div>
</template>

<script>
import { useLoadHrs } from '@/firebase'
import { reactive } from 'vue'

export default {
  setup() {
    const form = reactive({ email: '', password: '' })
    const users = useLoadHrs()

    return { form, users }
  },
  methods: {
    onLogin() {
      const loginValidation = _.find(this.users, {
        password: this.form.password,
        email: this.form.email,
      })
      if (typeof loginValidation === 'object') {
        this.isLoginValid = true
      } else {
        this.isLoginValid = false
      }

      console.log('this.isLoginValid', this.isLoginValid)
      console.log('loginValidation', loginValidation, typeof loginValidation) //if wrong it will return undefined, else object
    },
    data() {
      return {
        isLoginValid: false,
      }
    },
  },
}
</script>

<style lang="scss" scoped>
@import url('https://fonts.googleapis.com/css?family=Roboto&display=swap');

$background-color: #d7ccc8;
$font-family: 'Roboto', sans-serif;

@mixin btn($fontcolor: #fafafa) {
  font-family: 'Roboto', sans-serif;
  font-size: 15px;
  outline: 0;
  border: 0;
  width: 100%;
  padding: 15px;
  background: #ff5722;
  color: $fontcolor;
  text-transform: uppercase;
}

@mixin message($fontcolor: #90a4ae) {
  color: $fontcolor;
  text-align: center;
  font-family: 'Roboto', sans-serif;
  font-size: 14px;
}

@mixin input($bkgnd: #f5f5f5) {
  font-family: $font-family;
  width: 100%;
  border: 0;
  margin: 0 0 15px;
  padding: 15px;
  outline: 0;
  font-size: 15px;
  text-align: center;
  box-sizing: border-box;
  background: $bkgnd;
}

body {
  font-family: $font-family;
  background: $background-color;
}

.container {
  padding: 8% 0 0;
  width: 365px;
  margin: auto;
}

.form {
  position: relative;
  z-index: 1;
  max-width: 350px;
  margin: 0 auto 100px;
  padding: 45px;
  background: #ffffff;
}

.form {
  input {
    @include input;

    ::placeholder {
      color: #90a4ae;
    }
  }

  .btn {
    @include btn;
  }

  .message {
    @include message;
    a {
      text-decoration: none;
      color: #00bfa5;
    }
  }
}

.form .register-form {
  display: none;
}
</style>
