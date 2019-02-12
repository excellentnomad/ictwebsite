<template>
  <div>
    <v-form>
      <v-container fluid>
        <v-layout justify-center>
          <v-flex xs12 sm10 md8 lg6>
            <v-text-field
              v-model="firstname"
              :error-messages="firstnameErrors"
              :counter="15"
              label="First name"
              required
              @input="$v.firstname.$touch()"
              @blur="$v.firstname.$touch()"
            ></v-text-field>
            <v-text-field
              v-model="lastname"
              :error-messages="lastnameErrors"
              :counter="15"
              label="Last name"
              required
              @input="$v.lastname.$touch()"
              @blur="$v.lastname.$touch()"
            ></v-text-field>
            <v-text-field
              v-model="email"
              :error-messages="emailErrors"
              label="E-mail"
              required
              @input="$v.email.$touch()"
              @blur="$v.email.$touch()"
            ></v-text-field>
            <v-text-field
              v-model="password1"
              :error-messages="password1Errors"
              :append-icon="show1 ? 'visibility_off' : 'visibility'"
              :type="show1 ? 'text' : 'password'"
              label="Password"
              hint="At least 6 characters"
              required
              counter
              @click:append="show1 = !show1"
              @input="$v.password1.$touch()"
              @blur="$v.password1.$touch()"
            ></v-text-field>
            <v-text-field
              v-model="password2"
              :error-messages="password2Errors"
              :append-icon="show2 ? 'visibility_off' : 'visibility'"
              :type="show2 ? 'text' : 'password'"
              label="Re-enter password"
              required
              counter
              @click:append="show2 = !show2"
              @input="$v.password2.$touch()"
              @blur="$v.password2.$touch()"
            ></v-text-field>
            <v-flex row class="mt-2 pt-2">
              <v-btn @click="submit">submit</v-btn>
              <v-btn @click="clear">clear</v-btn>
            </v-flex>
          </v-flex>
        </v-layout>
      </v-container>
    </v-form>
  </div>
</template>
<script>
import { validationMixin } from 'vuelidate'
import { required, maxLength, email, minLength, sameAs } from 'vuelidate/lib/validators'

export default {
  mixins: [validationMixin],

  validations: {
    firstname: { required, maxLength: maxLength(15) },
    lastname: { required, maxLength: maxLength(15) },
    email: { required, email },
    password1: { required, minLength: minLength(6)},
    password2: { sameAsPassword: sameAs('password1') }
  },

  data: () => ({
    firstname: '',
    lastname: '',
    email: '',
    show1: false,
    show2: false,
    password1: '',
    password2: ''
  }),
  computed: {
    firstnameErrors() {
      const errors = []
      if (!this.$v.firstname.$dirty) return errors
      !this.$v.firstname.maxLength &&
        errors.push('Fist name must be at most 15 characters long')
      !this.$v.firstname.required && errors.push('First name is required.')
      return errors
    },
    lastnameErrors() {
      const errors = []
      if (!this.$v.lastname.$dirty) return errors
      !this.$v.lastname.maxLength &&
        errors.push('Last name must be at most 15 characters long')
      !this.$v.lastname.required && errors.push('Last name is required.')
      return errors
    },
    emailErrors() {
      const errors = []
      if (!this.$v.email.$dirty) return errors
      !this.$v.email.email && errors.push('Must be valid e-mail')
      !this.$v.email.required && errors.push('E-mail is required')
      return errors
    },
    password1Errors() {
      const errors = []
      if (!this.$v.password1.$dirty) return errors
      !this.$v.password1.minLength &&
        errors.push('Password must be at least 6 characters long')
      !this.$v.password1.required && errors.push('Password is required.')
      return errors
    },
    password2Errors() {
      const errors = []
      if (!this.$v.password2.$dirty) return errors
      !this.$v.password2.sameAsPassword &&
        errors.push('Passwords do not match, reenter your password.')
      return errors
    }
  },
  methods: {
    submit() {
      this.$v.$touch()
    },
    clear() {
      this.$v.$reset()
      this.firstname = ''
      this.lastname = ''
      this.email = ''
    }
  }
}
</script>

