<template>
  <div id="app">
    <div class="App">
      <form action="" class="form">
        <div class="form__header">
          <div class="form__title">Регистрация</div>
          <div class="form__note">Уже есть аккаунт? <a href="/">Войти</a></div>
        </div>
        <div class="form__content">
          <div class="form__block">
            <label htmlFor="name" class="form__label">Имя</label>
            <input
              id="name"
              name="name"
              type="text"
              class="form__input"
              placeholder="Введите Ваше имя"
              v-model="name"
              @blur="validateName"
            />
            <span>{{nameError}}</span>
          </div>
          <div class="form__block">
            <label htmlFor="email" class="form__label">Email</label>
            <input
              id="email"
              name="email"
              type="text"
              class="form__input"
              placeholder="Введите Ваш email"
              v-model="email"
              @blur="validateEmail"
            />
            <span>{{emailError}}</span>
          </div>
          <div class="form__block">
            <label htmlFor="phone" class="form__label">Номер телефона</label>
            <input
              id="phone"
              name="phone"
              type="text"
              class="form__input"
              placeholder="Введите номер телефона"
              v-model="phone"
              @blur="validatePhone"
            />
            <span>{{phoneError}}</span>
          </div>
          <label htmlFor="language" class="form__label">Язык</label>
          <input
            id="language"
            name="language"
            type="hidden"
            v-model="selectedLanguage"
          />
          <div class="select">
            <div class="select__selected" @click="() => openLanguages = true">{{selectedLanguage}}</div>
            <div class="select__languages" v-bind:class="{'select__languages--active' : openLanguages}">
              <ul>
                <li v-for="language in languages" @click="changeLanguage(language)" :key="language">{{language}}</li>
              </ul>
            </div>
          </div>
          <label
            htmlFor="accept"
            class="form__check">
            <input
              name="accept"
              id="accept"
              type="checkbox"
              v-model="accept"
            />
            <span class="form__checkmark"></span>Принимаю <a href="/">условия</a> использования
          </label>
          <button 
            type="submit" 
            class="btn" 
            v-bind:disabled="disabled"
          >Зарегистрироваться</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import './App.scss'


export default {
  name: "App",
  data() {
    return {
      name: '',
      nameError: ' ',
      email: '',
      emailError: ' ',
      phone: '',
      phoneError: ' ',
      languages: [
        'Русский',
        'Английский',
        'Китайский',
        'Испанский'
      ],
      accept: false,
      selectedLanguage: 'Русский',
      openLanguages: false
    }
  },
  methods: {
    changeLanguage: function(language) {
      this.selectedLanguage = language;
      this.openLanguages = false;
    },
    validateName: function() {
      const re = new RegExp('[^a-zа-я\\s\\-]+');
      if (this.name === '') {
        this.nameError = 'поле “Имя” не может быть пустым';
      } else if (re.test(String(this.name).toLowerCase())) {
        this.nameError = 'поле “Имя” не может содержать цифры и символы кроме пробела и дефиса';
      } else {
        this.nameError = '';
      }
    },
    validateEmail: function() {
      const re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
      if (!re.test(String(this.email).toLowerCase())) {
        this.emailError = 'не корректный email';
      } else {
        this.emailError = '';
      }
    },
    validatePhone: function() {
      const re = /^(8|\+7|7)[\\-]?\(?\d{3}\)?[\\-]?[\d]{3}[\\-]?[\d]{2}[\\-]?[\d]{2}$/;
      if (!re.test(String(this.phone).toLowerCase())) {
        this.phoneError = 'не корректный номер телефона';
      } else {
        this.phoneError = '';
      }
    }
  },
  computed: {
    disabled() {
      return !(this.accept && !this.nameError && !this.emailError && !this.phoneError);
    },
  }
};
</script>
