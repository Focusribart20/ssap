<template>
  <v-container class="fill-height" fluid>
    <v-row align="center" class="justify-center" justify="center" no-gutters>
      <v-col cols="12" class="d-flex justify-space-around">
        <v-card class="elevation-12" width="400">
          <v-toolbar prominent :src="image" flat>
            <v-toolbar-title color="white" dense>
              <img height="100px" width="100" class="mt-6" src="../assets/images/logo.png" alt="" />
            </v-toolbar-title>
            <v-spacer></v-spacer>
          </v-toolbar>
          <v-card-text>
            <v-form @submit.prevent="login" id="check-login-form" class="mt-3" v-model="valid">
              <v-container>
                <v-row>
                  <v-col cols="14" sm="14">
                    <v-text-field rounded label="Username" placeholder="e.g. demo" v-model="payload.username"
                      prepend-inner-icon="person" :rules="[rules.required]" value="user" required outlined>
                    </v-text-field>

                    <v-text-field rounded v-model="payload.password" prepend-inner-icon="lock"
                      :append-icon="show1 ? 'visibility' : 'visibility_off'" :rules="[rules.required, rules.min]"
                      :type="show1 ? 'text' : 'password'" name="input-10-1" label="Password" placeholder="e.g ********"
                      hint="At least 8 characters" counter @click:append="show1 = !show1" required outlined>
                    </v-text-field>
                  </v-col>
                </v-row>
              </v-container>
            </v-form>
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn block large rounded color="primary" type="submit" :disabled="!valid" form="check-login-form">Login
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script lang="js">
import { mapGetters } from "vuex"
export default {
  meta: {
    auth: {
      requiresAuth: false
    }
  },
  layout: "home",
  data: () => ({
    valid: false,
    show1: false,
    show2: true,
    show3: false,
    show4: false,
    payload: {
      password: "Password1!",
      username: "selfservice",
    },
    image: "https://vicsguide.com/wp-content/uploads/2021/07/Best-loan-apps.jpg",
    rules: {
      required: value => !!value || "Required.",
      min: v => v.length >= 8 || "Min 8 characters",
      emailMatch: () => "The email and password you entered don't match"
    }
  }),
  computed: {

  },
  methods: {
    login() {
      this.$store.dispatch("_authenticate", this.payload)
    },
    nativateToHere(id) {
      this.$router.push('/' + id);
    },
  },

  beforeMount() {
    if (!this.isAuthenticated) {
      this.$router.push("/");
    }
  },
  computed: {
    ...mapGetters({
      isAuthenticated: "isAuthenticated"
    })
  }
};
</script>
