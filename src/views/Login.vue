<template>
  <form @submit.prevent="submit" class="card auth-card">
    <div class="card-content">
      <span class="card-title">Домашняя бухгалтерия</span>
      <div class="input-field">
        <input
          @blur="v$.email.$touch()"
          v-model.trim="email"
          id="email"
          type="text"
          :class="{
            invalid:
              (v$.email.$dirty && v$.email.required.$invalid) ||
              (v$.email.$dirty && v$.email.email.$invalid),
          }"
        />

        <label for="email">Email</label>
        <small
          v-if="v$.email.$dirty && v$.email.required.$invalid"
          class="helper-text invalid"
          >Поле не может быть пустым!</small
        >
        <small
          v-else-if="v$.email.$dirty && v$.email.email.$invalid"
          class="helper-text invalid"
          >Не корректный email!</small
        >
      </div>
      <div class="input-field">
        <input
          v-model.trim="password"
          @blur="v$.password.$touch()"
          id="password"
          type="password"
          :class="{
            invalid:
              (v$.password.$dirty && v$.password.required.$invalid) ||
              (v$.password.$dirty && !v$.password.minLength),
          }"
        />

        <label for="password">Пароль</label>
        <small
          v-if="v$.password.$dirty && v$.password.required.$invalid"
          class="helper-text invalid"
          >Поле не может быть пустым!</small
        >

        <small
          v-else-if="v$.password.$dirty && v$.password.minLength.$invalid"
          class="helper-text invalid"
          >Пароль должен состоять не менее
          {{ v$.password.minLength.$params.min }} символов!</small
        >
      </div>
    </div>
    <div class="card-action">
      <div>
        <button
          @click="submitHandlers"
          class="btn waves-effect waves-light auth-submit"
          type="submit"
        >
          Войти
          <i class="material-icons right">send</i>
        </button>
      </div>

      <p class="center">
        Нет аккаунта?
        <router-link to="/">Зарегистрироваться</router-link>
      </p>
    </div>
  </form>
</template>
<script>
//import { reactive } from "@vue/composition-api";
import { email, required, minLength } from "@vuelidate/validators";
import { useVuelidate } from "@vuelidate/core";

export default {
  setup() {
    return { v$: useVuelidate() };
  },
  data() {
    return {
      email: "",
      password: "",
    };
  },
  validations() {
    return {
      password: { required, minLength: minLength(6) },

      email: { required, email },
    };
  },
  mounted() {
    // console.log(this.v$.email.$invalid,'email');
  },
  methods: {
    submit() {
      if (!this.v$.email.$invalid && !this.v$.password.$invalid) {
        console.log("Все поля  валидны");
        this.$router.push("#");
      } else {
        console.log("поле НЕ Валидный!!");
      }
    },
    submitHandlers() {},
  },
};
</script>
