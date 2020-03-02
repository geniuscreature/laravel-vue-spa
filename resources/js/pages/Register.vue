<template>
    <section class="index">
        <section class="info">
            <div class="info-top">
                <div class="info-title">
                    <img src="images/logo/logo_white.svg" alt="notes app logo" class="logo">
                    <h1 class="title">ote.it</h1>
                </div>
                <div class="info-lang">
                    <a href="#" class="lang ru">RU</a>
                </div>
            </div>
            <div class="info-content">
                <ul class="list">
                    <li class="list-thing"><img src="/images/icons/pen.svg" class="list-thing-img">Note ideas, write product list</li>
                    <li class="list-thing"><img src="/images/icons/remind.svg" class="list-thing-img">Set reminders: birthdays, meetings, feeding the cat</li>
                    <li class="list-thing"><img src="/images/icons/stages.svg" class="list-thing-img">Complete projects in stages</li>
                    <li class="list-thing"><img src="/images/icons/passw.svg" class="list-thing-img">Keep your important entries with a password</li>
                    <li class="list-thing"><img src="/images/icons/voice.svg" class="list-thing-img">Create voice notes</li>
                </ul>
            </div>
            <div class="info-contacts">
                Created by me
            </div>
        </section>
        <section class="reg">
            <div class="alert alert-danger" v-if="has_error && !success">
                <p v-if="error == 'registration_validation_error'">Erreur(s) de validation, veuillez consulter le(s) message(s) ci-dessous.</p>
                <p v-else>Erreur, impossible de s'inscrire pour le moment. Si le problème persiste, veuillez contacter un administrateur.</p>
            </div>
            <form autocomplete="on" @submit.prevent="register" v-if="!success" method="post" id="form" class="form">
                <h2 class="form-title registration">Registration</h2>
<!--                <div class="form-group form-name" v-bind:class="{ 'has-error': has_error && errors.name }">-->
<!--                    <input type="text" id="name" class="form-control form-email-input reg-input" placeholder="Your name" v-model="name">-->
<!--                    <span class="help-block" v-if="has_error && errors.name">{{ errors.name }}</span>-->
<!--                </div>-->
                <div class="form-group form-email" v-bind:class="{ 'has-error': has_error && errors.email }">
                    <input type="email" id="email" class="form-email-input reg-input" placeholder="Your email" v-model="email">
                    <span class="help-block" v-if="has_error && errors.email">{{ errors.email }}</span>
                </div>
                <div class="form-group form-password" v-bind:class="{ 'has-error': has_error && errors.password }">
                    <input type="password" id="password" class="form-password-input reg-input" v-model="password" placeholder="Your password">
                    <span class="help-block" v-if="has_error && errors.password">{{ errors.password }}</span>
                </div>
                <div class="form-group form-password" v-bind:class="{ 'has-error': has_error && errors.password }">
                    <input type="password" id="password_confirmation" class="form-password-input reg-input" v-model="password_confirmation" placeholder="Password again">
                </div>
                <div class="form-btn">
                    <button type="submit" class="form-btn-reg">Registration</button>
                </div>
                <div class="form-have-account">
                    <router-link to="/login" class="form-have-account-link">
                        Have an account? Log in
                    </router-link>
                </div>
            </form>
        </section>
    </section>
</template>
<script>
  export default {
    data() {
      return {
        name: '',
        email: '',
        password: '',
        password_confirmation: '',
        has_error: false,
        error: '',
        errors: {},
        success: false,
      }
    },

    methods: {
      register() {
        let app = this
        this.$auth.register({
          data: {
            email: app.email,
            password: app.password,
            password_confirmation: app.password_confirmation
          },
          success: function () {
            app.success = true
            this.$router.push({name: 'login', params: {successRegistrationRedirect: true}})
          },
          error: function (res) {
            console.log(res.response.data.errors)
            app.has_error = true
            app.error = res.response.data.error
            app.errors = res.response.data.errors || {}
          }
        })
      }
    },
  }
</script>
