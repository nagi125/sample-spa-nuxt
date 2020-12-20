<template>
  <b-container class="animated fadeIn mt-3">
    <b-alert variant="danger" :show="isFailure" dismissible @dismissed="isFailure=false">
      {{ errorMessage }}
    </b-alert>
    <b-row class="justify-content-center">
      <b-col md="8">
        <b-card header="管理画面Login">
          <b-card-body>
            <b-form name="login" @submit.prevent="login()">
              <b-row class="justify-content-md-center">
                <b-col col md="6">
                  <b-form-group>
                    <b-form-input type="email" placeholder="Email" v-model="form.email"></b-form-input>
                  </b-form-group>
                </b-col>
              </b-row>
              <b-row class="justify-content-md-center">
                <b-col col md="6">
                  <b-form-group>
                    <b-form-input type="password" placeholder="Password" v-model="form.password"></b-form-input>
                  </b-form-group>
                </b-col>
              </b-row>
              <div class="text-center">
                <b-button class="px-4" type="submit" variant="primary">Login</b-button>
              </div>
            </b-form>
          </b-card-body>
        </b-card>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
export default {
  name: 'login',
  layout: 'clean',

  data() {
    return {
      form: {
        email: '',
        password: '',
      },
      isFailure: false,
      errorMessage: '',
    }
  },

  methods: {
    async login() {
      try {
        const res = await this.$auth.loginWith('local', { data: this.form });

      } catch(err) {
        console.log(err);
        this.isFailure = true;
        this.errorMessage = 'EmailかPasswordが間違っています';
      }
    },
  },
};
</script>
