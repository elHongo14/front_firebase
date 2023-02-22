<template>
    <v-card class="cardLogin">
        <v-card-title class="title">Iniciar Sesión</v-card-title>
        <v-card-text>
            <v-row justify="center">
                <v-col cols="4" align-self="center">
                    <img src="../../assets/images/user.jpg" class="imgLogin">
                </v-col>
                <v-col cols="8" align-self="center">
                    <v-form ref="formLogin">
                <v-text-field label="Correo Electrónico" 
                              placeholder="Correo Electrónico"
                              v-model="correoElectronico"
                              :rules="validarCorreo"
                />
                <v-text-field label="Contraseña" 
                              placeholder="Contraseña"
                              v-model="password"
                              :rules="validarPassword"
                />
            </v-form>
                </v-col>
            </v-row>
            
        </v-card-text>
        <v-card-actions>
            <v-btn
            class="btnLogin"
            rounded
            block
            @click="loginBackend"
            >
                Iniciar
            </v-btn>
        </v-card-actions>
    </v-card>
</template>

<script>
export default {
    data() {
        return {
            correoElectronico: '',
            validarCorreo: [
            v => !v || /^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/.test(v) || 'E-mail must be valid'
            ],
            password:'',
            validarPassword: [
                value => value.length >= 6 || 'Min 6 characters'
            ]
        }
    },
    methods: {
        async loginBackend () {
            const valid = this.$refs.formLogin.validate()
            if (valid) {
                const sendData = {
                    email: this.correoElectronico,
                    password: this.password
                }
                await this.$auth.loginWith('local', {
                    data: sendData
                }).then(async (res) => {
                    console.log('respuesta del back:', res)
                    if (res.data.error == null) {
                        this.$router.push('/dashboard')
                    }
                }).catch((error) => {
                    console.log('error: ', error)
                })
            }else {
                alert('no cumpliste las reglas')
            }
        }
    }
}
</script>

<style scoped>
.cardLogin {
    background-color: #6d60a5;
    border-radius: 10px;
    width: 500px;
    height: 300px;
}

.imgLogin {
    width: 100%;
    height: 100%;
    border-color: #362f5a;
    border-style: dotted;
    border-radius: 20px;
}

.btnLogin {
    background-color: #362f5a  !important;
    color: white !important;
    font-family: Arial, Helvetica, sans-serif;
    font-style: italic;
}

.title {
    font-size: 30px;
    justify-content: center;
    color: white;
    font-weight: 700;
    font-family: Arial, Helvetica, sans-serif;
    font-style: italic;
}

</style>