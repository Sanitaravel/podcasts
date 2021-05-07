<template>
  <v-container fill-height>
    <v-row justify="center" align="center">
      <v-col align="center">
        <h1>Listen Podcasts. Everywhere.</h1>
        <v-img
          src="https://faithandleadership.com/sites/default/files/styles/article/public/field/image/listen_podcast_m.png?itok=GG7-tpli"
        />
      </v-col>
      <v-divider vertical></v-divider>
      <v-col align="center">
        <v-list flat>
          <v-list-item fluid>
            <v-container>
              <v-form ref="form" v-model="valid" lazy-validation>
                <v-text-field
                  v-model="name"
                  :rules="nameRules"
                  label="Username"
                  required
                  autocomplete="false"
                ></v-text-field>

                <v-text-field
                  v-model="password"
                  label="Password"
                  :rules="passwordRules"
                  required
                  autocomplete="false"
                  type="password"
                ></v-text-field>

                <v-container>
                  <v-btn outlined :disabled="!valid" text @click="validate()">
                    LOGIN
                  </v-btn>
                </v-container>
              </v-form>
            </v-container>
          </v-list-item>
          <v-divider></v-divider>
          <v-list-item>
            <v-container align-content-center>
              <h2>OR</h2>
            </v-container>
          </v-list-item>
          <v-divider />
          <v-list-item>
            <v-container align-content-center>
              <v-btn text>Register</v-btn>
            </v-container>
          </v-list-item>
        </v-list>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    valid: false,
    name: '',
    nameRules: [(v) => !!v || 'Username is required'],
    password: '',
    passwordRules: [(v) => !!v || 'Password is required'],
  }),

  methods: {
    validate() {
      this.$refs.form.validate()
    },
    reset() {
      this.$refs.form.reset()
    },
    resetValidation() {
      this.$refs.form.resetValidation()
    },
  },
}
</script>
