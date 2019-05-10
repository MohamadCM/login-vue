<template>
  <div id="app">
    <transition name="fade">
  <v-app v-if="!loggedIn">
    <v-toolbar app color = "blue-grey darken-2">
      <v-toolbar-title class="headline text-uppercase">
      </v-toolbar-title>
      <v-btn><p>logout</p></v-btn>
    </v-toolbar>
      <v-layout align-center justify-center row fill-height >
        <v-flex xs12 sm10 md5 lg4>
          <v-container class="text-xs-center">
            <transition name="fade">
            <v-card tile v-bind:class="{ [`elevation-${elevation}`]: true }">
              <v-card-title primary-title>
                <v-layout align-center justify-center row fill-height>
                  <h3 v-if="!signup & !forgot">ورود</h3>
                  <h3 v-if="forgot">فراموشی پسورد</h3>
                  <h3 v-if="signup">!ثبت نام</h3>
                </v-layout>
              </v-card-title>

              <v-form>
                <v-layout mr-3 ml-3>
                   <v-text-field v-if="!forgot" prepend-icon="person" name="Username" label="نام کاربری"  align="right" v-model="username"></v-text-field>
                </v-layout>
                <v-layout mr-3 ml-3>
                <v-text-field v-if="!forgot" prepend-icon="lock" name="Password" label="پسورد" type="password" v-model="password"></v-text-field>
                </v-layout>
                <v-layout mr-3 ml-3>
                <transition name="fade">
                  <v-text-field v-if="forgot" prepend-icon="email" name="email" label="ایمیل" v-model="email"></v-text-field>
                  <v-text-field v-if="signup" prepend-icon="email" name="email" label="ایمیل" v-model="email"></v-text-field>
                </transition>
                </v-layout>
                <v-layout align-center justify-center row fill-height>
                  <transition name="fade">

                <table>
                  <tr>
                    <td><span><v-checkbox v-if="!signup & !forgot" v-model="remember" ></v-checkbox></span></td>
                    <td><span v-if="!signup & !forgot" @click="remember = !remember" disabled="">بخاطر سپردن ورود</span></td>
                    <td><span><v-btn v-if="!forgot & !signup" normal flat color="blue-grey darken-3" @click="forgot = !forgot">فراموشی پسورد</v-btn></span></td>
                    <v-btn v-if="forgot" normal flat color="blue-grey darken-3" @click="forgotPassword">ارسال ایمیل</v-btn>
                    <v-btn v-if="forgot" normal flat color="blue-grey darken-3" @click="forgot = !forgot">بازگشت</v-btn>
                  </tr>
                </table>
                  </transition>
                </v-layout>
                <v-btn large flat v-if="!forgot" color="blue-grey darken-3" @click="register" align-center justify-center>!ثبت نام</v-btn>
                <v-btn v-if="signup" normal flat color="blue-grey darken-3" @click="signup = !signup">بازگشت</v-btn>
                <v-card-actions>
                  <v-btn primary large block flat color="blue-grey darken-3" v-if="!signup & !forgot" @click="checkLogin">
                    <router-link to="/main"></router-link>ورود</v-btn>
                </v-card-actions>
              </v-form>

            </v-card>
            </transition>
          </v-container>
        </v-flex>
      </v-layout>
  </v-app>
    </transition>

    <v-container>
        <v-toolbar app color = "blue-grey darken-2">
          <v-toolbar-title class="headline text-uppercase">
          </v-toolbar-title>
        </v-toolbar>


      <v-toolbar app color = "blue-grey darken-2">
        <v-toolbar-title class="headline text-uppercase">
        </v-toolbar-title>
        <v-btn color="light-blue lighten-3"
                v-if="loggedIn"
                @click="loggedIn = !loggedIn"
                flat
        >
          <v-icon
                  color="light-blue lighten-3"
                  small
                  class="mx-2"
          >
            exit_to_app
          </v-icon>
          <p class="hidden-xs-only mt-2" >
            خروج
          </p>
        </v-btn>
      </v-toolbar>


      <!-- Code HERE!!!! -->





    </v-container>
  </div>



</template>

<script>

export default {
  name: 'App',
  components: {
  },

  data :()=> ({
      elevation:15,
      username: '',
      password: '',
      email: '',
      forgot: false,
      signup: false,
      loggedIn: false,
      remember: true

  }) , methods :{
    checkLogin : function () {
      this.loggedIn = !this.loggedIn
    },
    register : function () {
      this.signup = !this.signup;
    },
    forgotPassword:function () {
      this.forgot = !this.forgot;
    }
  }
}
</script>

<style>
  .fade-enter-active, .fade-leave-active {
    transition: opacity .4s;
  }
  .fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
    opacity: 0;
  }
  div{
    font-family: Arial,sans-serif;
  }
  .v-progress-circular{
  margin: 1rem}
</style>
