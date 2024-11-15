<template>
    <v-app>
        <v-main>
            <v-container class="d-flex justify-center align-center" style="height: 100vh">
                <v-card style="width: 20%">
                    <v-card-title>Login</v-card-title>
                    <v-card-text>
                        <v-form>
                            <v-text-field label="Username" outlined v-model="username">
                            </v-text-field>

                            <v-text-field
                                v-model="password"
                                label="Password"
                                outlined
                                :type="showPassword ? 'text' : 'password'"
                            >
                                <template v-slot:append>
                                    <v-icon
                                        @mousedown="togglePasswordVisibility(true)"
                                        @mouseup="togglePasswordVisibility(false)"
                                        @mouseleave="togglePasswordVisibility(false)"
                                    >
                                        {{ showPassword ? 'mdi-eye' : 'mdi-eye-off' }}
                                    </v-icon>
                                </template>
                            </v-text-field>

                            <v-progress-linear
                                :color="strengthColor"
                                :model-value="passwordStrength"
                            >
                            </v-progress-linear>
                        </v-form>
                    </v-card-text>
                </v-card>
            </v-container>
        </v-main>
    </v-app>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'
import '@mdi/font/css/materialdesignicons.css'
import commonPasswordsList from '@/assets/commonPasswordsList.json'

const username = ref('')
const password = ref('')
const showPassword = ref(false)
const commonPasswords = new Set<string>(commonPasswordsList)

const passwordStrength = computed(() => {
    let value = 0

    if (
        username.value.length > 4 &&
        password.value.toLowerCase().includes(username.value.toLowerCase())
    ) {
        return value
    }

    if (password.value.length < 8) {
        return value
    } else if (password.value.length < 12) {
        value += 20
    } else value += 35

    if (containsUpperAndLower(password.value)) {
        value += 25
    }

    if (containsNumber(password.value)) {
        value += 25
    }

    if (containsSpecialCharacter(password.value)) {
        value += 15
    }

    if (commonPassword(password.value)) {
        value -= 20
    }

    return value
})

const strengthColor = computed(() => {
    if (passwordStrength.value < 30) return 'red'
    if (passwordStrength.value < 70) return 'orange'
    return 'green'
})

function togglePasswordVisibility(visible: boolean) {
    showPassword.value = visible
}

function containsUpperAndLower(str: string) {
    return /[a-z]/.test(str) && /[A-Z]/.test(str)
}

function containsNumber(str: string) {
    return [...str].some((c) => /[0-9]/.test(c))
}

function containsSpecialCharacter(str: string) {
    return /[^a-zA-Z0-9]/.test(str)
}

function commonPassword(str: string) {
    return commonPasswords.has(str)
}
</script>

<style></style>
