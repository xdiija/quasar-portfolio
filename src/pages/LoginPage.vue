<template>
  <q-page class="flex flex-center bg-primary">
    <q-card
      style="width: 300px; height: auto; display: flex; flex-direction: column; align-items: center"
    >
      <q-img src="../assets/login.png" ratio="1" width="200px" />

      <q-card-section class="q-pt-none full-width">
        <q-input filled v-model="login.nick" label="Nickname" />
        <q-input class="q-mt-sm" v-model="login.password" filled label="Password" :type="login.isPwd ? 'password' : 'text'">
        <template v-slot:append>
          <q-icon
            :name="login.isPwd ? 'visibility_off' : 'visibility'"
            class="cursor-pointer"
            @click="login.isPwd = !login.isPwd"
          />
        </template>
      </q-input>
      </q-card-section>

      <q-card-actions class="full-width">
        <q-btn flat class="q-mx-sm" color="primary" label="Registrar" @click="$router.push('/register')" style="width: 100%" />
      <div class="q-pa-md">
        <q-checkbox label="Remember me" v-model="val"  />
      </div>
        <q-btn class="q-mx-sm" color="primary" label="Login" @click="$router.push({ name: 'home' })" style="width: 100%"/>
      </q-card-actions>
      <q-card-actions class="full-width">
        <q-btn flat no-caps class="q-mx-sm" color="primary" label="Esqueci minha senha" @click="$router.push({ name: 'esqueciSenha' })" style="width: 100%"/>
      </q-card-actions>
    </q-card>

    <q-card class="my-card">
      <q-img src="https://cdn.quasar.dev/img/parallax2.jpg" basic>
        <div class="absolute-bottom text-subtitle2 text-center">
          Title
        </div>
      </q-img>
    </q-card>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data () {
    return {
      login: {
        nick: '',
        password: '',
        isPwd: true
      }
    }
  },
  methods: {
    logar () {
      this.$axios.post('/api/login', this.login)
        .then((response) => {
          console.log('sucesso :', response)
          this.$router.push({ name: 'home' })
        })
        .catch(erro => {
          alert(JSON.stringify(erro))
          console.log('erro: ', erro)
        })
    }
  }
}
</script>
