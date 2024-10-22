<script setup>
    import { useForm, useField } from 'vee-validate';
    import { loginSchema as validationSchema } from '@/validation/loginSchema';
    import { useFirebaseAuth } from 'vuefire';
    import { signInWithEmailAndPassword } from 'firebase/auth';

    const { handleSubmit } = useForm({validationSchema})
    const auth = useFirebaseAuth()

    const email = useField('email')
    const password = useField('password')

    const submit = handleSubmit((values)=>{
        signInWithEmailAndPassword(auth, values.email, values.password)
        .then((userCredential)=>{
            console.log(userCredential)
        })
        .catch(error => {
            console.error(error.code)
            console.error(error.message)
        })
    })





</script>

<template>

    <v-card
        flat
        max-width="600"
        class="mx-auto my-10"
    >
        <v-card-title
            class="text-h4 font-weight-bold"
            tag="h3"
        >
            Iniciar Sesión
        </v-card-title>
        <v-card-subtitle
            class="text-h5"
        >
            Inicia sesión con tu cuenta
        </v-card-subtitle>

        <v-form>
            <v-text-field 
                type="email"
                label="Email"
                bg-color="blue-grey-lighten-5"
                variant="outlined"
                class="mb-4"
                v-model="email.value.value"
                :error-messages="email.errorMessage.value"
            />
            <v-text-field 
                type="password"
                label="Contraseña"
                bg-color="blue-grey-lighten-5"
                hint="Ingresa la contraseña de tu cuenta para acceder al sitio"
                variant="outlined"
                class="mb-4"
                v-model="password.value.value"
                :error-messages="password.errorMessage.value"
            />
            <v-btn
                density="default"
                color="pink-accent-3"
                block
                @click="submit"
            >
                Iniciar Sesión
            </v-btn>
    
        </v-form>
    </v-card>



</template>

