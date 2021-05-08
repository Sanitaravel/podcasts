<template>
  <v-main>
    <v-container fill-height>
      <v-row justify="center">
        <v-col>
          <v-container fill-height>
            <v-row align="center" justify="center">
              <h1>Register and enjoy!</h1>
            </v-row>
          </v-container>
        </v-col>
        <v-divider vertical></v-divider>
        <v-col>
          <v-container>
            <v-row justify="center">
              <v-form>
                <v-stepper v-model="e1">
                  <v-stepper-header>
                    <v-stepper-step :complete="e1 > 1" step="1">
                      Email
                    </v-stepper-step>

                    <v-divider></v-divider>

                    <v-stepper-step :complete="e1 > 2" step="2">
                      Username
                    </v-stepper-step>

                    <v-divider></v-divider>

                    <v-stepper-step :complete="e1 > 3" step="3">
                      Password
                    </v-stepper-step>

                    <v-divider></v-divider>

                    <v-stepper-step step="4"> Create account </v-stepper-step>
                  </v-stepper-header>

                  <v-stepper-items>
                    <v-stepper-content step="1">
                      <v-card class="mb-6">
                        <v-card-title>Enter your email!</v-card-title>
                        <v-card-text>
                          If you lose your password, we can recover it via your
                          email.
                        </v-card-text>

                        <v-card-actions>
                          <v-text-field
                            v-model="email"
                            :rules="[rules.required, rules.email]"
                            label="E-mail"
                            required
                          ></v-text-field>
                        </v-card-actions>
                      </v-card>

                      <v-btn
                        :disabled="!checkEmail"
                        color="primary"
                        @click="e1 = 2"
                      >
                        Continue
                      </v-btn>

                      <v-btn text> Cancel </v-btn>
                    </v-stepper-content>

                    <v-stepper-content step="2">
                      <v-card class="mb-6">
                        <v-card-title>Enter your username!</v-card-title>
                        <v-card-text>
                          This username you will see in system.
                        </v-card-text>

                        <v-card-actions>
                          <v-text-field
                            v-model="username"
                            :rules="[rules.required]"
                            label="Username"
                            required
                          ></v-text-field>
                        </v-card-actions>
                      </v-card>

                      <v-btn
                        :disabled="username === ''"
                        color="primary"
                        @click="e1 = 3"
                      >
                        Continue
                      </v-btn>

                      <v-btn text @click="e1 = 1"> Cancel </v-btn>
                    </v-stepper-content>

                    <v-stepper-content step="3">
                      <v-card class="mb-6">
                        <v-card-title>Enter your password!</v-card-title>
                        <v-card-text>
                          You know why you need password :)
                        </v-card-text>

                        <v-card-actions>
                          <v-text-field
                            v-model="password"
                            :rules="[rules.required, rules.min]"
                            label="Password"
                            required
                            :prepend-icon="show ? 'mdi-eye' : 'mdi-eye-off'"
                            :type="show ? 'text' : 'password'"
                            class="mr-2"
                            hint="At least 8 characters"
                            counter
                            @click:prepend="show = !show"
                          ></v-text-field>
                          <v-text-field
                            v-model="password_confirm"
                            label="Confirm password"
                            :type="show ? 'text' : 'password'"
                            required
                          ></v-text-field>
                        </v-card-actions>
                      </v-card>

                      <v-btn
                        :disabled="
                          password !== password_confirm ||
                          password === '' ||
                          password_confirm === ''
                        "
                        color="primary"
                        @click="e1 = 4"
                      >
                        Continue
                      </v-btn>

                      <v-btn text @click="e1 = 2"> Cancel </v-btn>
                    </v-stepper-content>

                    <v-stepper-content step="4">
                      <v-card class="mb-6">
                        <v-card-title>Check your details!</v-card-title>
                        <v-card-text>
                          Check if there is an error and you will not be able to
                          enter. It will be sad :(
                        </v-card-text>

                        <v-card-actions>
                          <v-container three-line>
                            <v-text-field
                              type="email"
                              :value="email"
                            ></v-text-field>
                            <v-text-field
                              type="text"
                              :value="username"
                            ></v-text-field>
                            <v-text-field
                              :prepend-inner-icon="
                                show ? 'mdi-eye' : 'mdi-eye-off'
                              "
                              :type="show ? 'text' : 'password'"
                              :value="password"
                              @click:prepend-inner="show = !show"
                            ></v-text-field>
                            <v-checkbox
                              v-model="checkbox"
                              label="Is correct?"
                            ></v-checkbox>
                          </v-container>
                        </v-card-actions>
                      </v-card>

                      <v-btn :disabled="!checkbox" color="primary">
                        Create Account
                      </v-btn>

                      <v-btn text @click="e1 = 3"> Cancel </v-btn>
                    </v-stepper-content>
                  </v-stepper-items>
                </v-stepper>
              </v-form>
            </v-row>
          </v-container>
        </v-col>
      </v-row>
    </v-container>
  </v-main>
</template>

<script>
export default {
  data() {
    return {
      e1: 1,
      show: false,
      checkbox: false,
      username: '',
      email: '',
      password: '',
      password_confirm: '',
      rules: {
        required: (value) => !!value || 'This field is required',
        min: (value) => value.length >= 8 || 'Min 8 characters',
        email: [
          (v) => !!v || 'E-mail is required',
          (v) => /.+@.+\..+/.test(v) || 'E-mail must be valid',
        ],
      },
    }
  },
  computed: {
    checkEmail() {
      return /.+@.+\..+/.test(this.email) && !!this.email
    },
  },
}
</script>
