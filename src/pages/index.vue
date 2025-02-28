<template>
    <v-app>
        <div class="py-15">
            <hero-section />
        </div>
        <div class="bg-primary py-15">
            <features-section />
        </div>
        <div class="py-15">
            <pricing-section />
        </div>
        <div class="py-15">
            <additional-section />
        </div>
        <div class="py-15">
            <faq-section />
        </div>

        <div class="py-15">
            <v-container>
                <div class="page-title mb-10 text-center">
                    <h1 class="text-h4 font-weight-bold mb-5">Ready to try YenHost?</h1>
                    <v-btn @click="goToRegisterPage" height="55px" rounded="lg" class="px-10" color="primary"
                        append-icon="mdi-arrow-right">Sign
                        up now</v-btn>
                </div>
            </v-container>
        </div>
    </v-app>
</template>

<script setup>
import { goToLoginPage, goToRegisterPage } from '@/utils.js';
</script>
