<template>
  <div class="outer">
    <div class="middle">
      <div class="inner">
        <form v-on:submit.prevent="submit()">
          <v-container fluid>
            <v-layout row wrap>
              <v-flex xs12 sm8 offset-sm2 md6 offset-md3 lg4 offset-lg4>
                <v-layout row wrap>
                  <v-flex xs12>
                    <v-text-field
                      label="Имя пользователя"
                      autofocus="autofocus"
                      v-model="username"
                      required
                    ></v-text-field>
                  </v-flex>
                  <v-flex xs12>
                    <v-text-field
                      name="password"
                      label="Пароль"
                      v-model="password"
                      :append-icon="passwordVisible ? 'visibility' : 'visibility_off'"
                      :append-icon-cb="() => (passwordVisible = !passwordVisible)"
                      :type="passwordVisible ? 'text' : 'password'"
                      required
                    ></v-text-field>
                  </v-flex>
                  <v-flex xs12>
                    <v-select
                      v-bind:items="userTypes"
                      item-text="name"
                      item-value="name"
                      v-model="userType"
                      return-object
                      label="Тип пользователя"
                      single-line
                      bottom
                    ></v-select>
                  </v-flex>
                  <v-flex xs12 cl text-xs-right>
                    <v-btn primary :loading="loading" type="submit">Регистрация</v-btn>
                  </v-flex>
                  <v-flex xs12>
                    <router-link replace to="/sign-in">Уже зарегистрированы?</router-link>
                  </v-flex>
                </v-layout>
              </v-flex>
            </v-layout>
          </v-container>
        </form>
      </div>
    </div>

    <v-snackbar
      :timeout="5000"
      :bottom="true"
      :right="true"
      v-model="snackbar"
    >
      Ошибка при регистрации
      <v-btn flat class="pink--text" @click.native="snackbar = false">Закрыть</v-btn>
    </v-snackbar>
  </div>
</template>

<script>
  import {signUp} from '../utils/auth'

  export default {
    name: 'sign-up-page',
    data() {
      return {
        username: "",
        password: "",
        userTypes: [
          {
            name: 'Исполнитель',
            value: "Performer",
          },
          {
            name: 'Заказчик',
            value: "Customer",
          }
        ],
        userType: {
          name: 'Исполнитель',
          value: "Performer",
        },
        passwordVisible: false,
        loading: false,
        snackbar: false,
      }
    },
    methods: {
      submit() {
        this.loading = true;
        signUp(this.username, this.password, this.userType.value).catch(error => {
          this.loading = false;
          this.snackbar = true;
          this.password = '';
        })
      }
    }
  }
</script>

<style>
  .outer {
    display: table;
    position: absolute;
    height: 100%;
    width: 100%;
  }

  .middle {
    display: table-cell;
    vertical-align: middle;
  }

  .inner {
    margin-left: auto;
    margin-right: auto;
    /*width: !*whatever width you want*!;*/
  }
</style>
