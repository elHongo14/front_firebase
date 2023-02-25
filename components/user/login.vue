<template>
    <form class="cardLogin">
        <v-card-title class="title">Iniciar Sesión</v-card-title>
        <v-card-text>
            <v-row justify="center">
                <v-col cols="4" align-self="center">
                    <img src="../../assets/images/user.jpg" class="imgLogin">
                </v-col>
                <v-col cols="8" align-self="center">
                    <v-form ref="formLogin">
                <v-text-field class="loginField"
                              label="Correo Electrónico" 
                              placeholder="Correo Electronico"
                              v-model="correoElectronico"
                              :rules="validarCorreo"
                />
                <v-text-field class="loginField"
                              label="Contraseña" 
                              placeholder="Password"
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
    </form>
</template>

<script>
export default {
    data() {
        return {
            correoElectronico: '',
            validarCorreo: [
            v => !v || /^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/.test(v) || 'Introduce un correo válido.'
            ],
            password:'',
            validarPassword: [
                value => value.length >= 6 || 'Introduce mínimo 6 caractéres'
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
                    if (res.data.alert !== 'Contraseña incorrecta') {
                        this.$router.push('/dashboard')
                    } else {
                        alert('Contraseña incorrecta!!')
                    }
                }).catch((error) => {
                    console.log('error: ', error)
                })
            }else {
                alert('Introduce los datos correctamente.')
            }
        }
    }
}
</script>

<style scoped>
.cardLogin {
    background: transparent;
    border-radius: 20px;
    border-color: white;
    border: 2px solid rgba(255, 255, 255, 0.5);
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
    backdrop-filter: blur(6px);
    width: 30rem;
    height: 300px;
    opacity: 0;
    
    animation: fadein 1s ease-in-out 1s forwards;
}

@keyframes fadein {
    0%{
        opacity: 0;
        transform: translateY(50px);
    }
    100%{
        opacity: 1;
    }
}

.imgLogin {
    width: 100%;
    height: 100%;
    border-color: #362f5a;
    border-style: dotted;
    border-radius: 20px;
}

.btnLogin {
    background-color: #6e0116  !important;
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

.loginField {
    font-family: Arial, Helvetica, sans-serif;
    font-style: italic;
}

</style>