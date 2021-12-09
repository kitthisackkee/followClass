<template>
     <v-layout wrap justify-center align-center fill-height>
    <v-flex md6>    
       <div class="form-login">
           <div class="text-center mb-6">
               <img width="120"  src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/53/Google_%22G%22_Logo.svg/800px-Google_%22G%22_Logo.svg.png" alt="">
            <h2 class="display-1" >ເຂົ້າສູ່ລະບົບ</h2>
        </div>
           <v-text-field
           v-model="frm.email"
          label="Email"
          append-icon="mdi-account-circle-outline" 
        ></v-text-field>
        <v-text-field
        v-model="frm.password"
          label="Passoword"
          :type="!showPass ? 'password' : 'text'"
          append-icon="mdi-eye-off" 
          @click:append="showPass = !showPass"
          @keyup.enter="doLogin()"
        ></v-text-field>
        <v-btn color="primary" block @click.prevent="doLogin" >ເຂົ້າສູ່ລະບົບ</v-btn>
       </div>
    </v-flex>
    <v-flex md6 class="blue lighten-5" fill-height>
      <v-layout justify-center align-center fill-height>
        <img src="@/assets/login.svg" alt="" class="img" />
      </v-layout>
    </v-flex>
  </v-layout>
</template>

<script>
export default {
    layout: 'blank',
    
    data(){
        return {
            showPass: false,
            frm: {
                email: '',
                password: ''
            }
        }
    },
    methods: {
        async doLogin() {
            try {
                let rs = await this.$axios.post('auth', this.frm)
                let { data } =  rs
                localStorage.setItem('user',JSON.stringify(data.user))
                localStorage.setItem('token',data.token)
                this.$toast('ເຂົ້າສູ່ລະບົບສຳເລັດ')
                this.$router.push('/')
            } catch (error) {
                this.$toast.error('ຊື່ຜູ້ໃຊ້ ຫຼື ລະຫັດບໍ່ຖືກຕ້ອງ')
            }
        }
    },
}
</script>

<style>
    .img {
        max-width: 100%;
        max-height: 400px;
    }
    .form-login {
        max-width: 400px;
        margin: 0 auto;
    }
</style>