<template>
    <v-footer class="py-6" elevation="15">
        <v-container>
            <v-row>
                <!-- Logo and About -->
                <v-col cols="12" md="4" class="d-flex flex-column align-center align-md-start">
                    <v-img :src="mainLogo" height="100%" width="100%" max-height="50px" max-width="150px" contain />
                    <p class="mt-3 text-body-2 text-center text-md-left">
                        YenHost provides fast, secure, and reliable hosting services for your online success.
                    </p>
                </v-col>

                <!-- Navigation Links -->
                <v-col cols="12" md="4">
                    <h3 class="text-h6 font-weight-bold mb-3">Quick Links</h3>
                    <v-list density="compact" class="bg-transparent">
                        <v-list-item v-for="item in footerLinks" :key="item.title" :to="item.link">
                            <v-list-item-title>{{ item.title }}</v-list-item-title>
                        </v-list-item>
                    </v-list>
                </v-col>

                <!-- Contact & Social Media -->
                <v-col cols="12" md="4">
                    <h3 class="text-h6 font-weight-bold mb-3">Get in Touch</h3>
                    <p class="text-body-2 mb-3">
                        <v-icon class="me-2">mdi-email</v-icon> support@yenhost.com
                    </p>
                    <p class="text-body-2 mb-3">
                        <v-icon class="me-2">mdi-phone</v-icon> +123 456 7890
                    </p>
                    <div class="d-flex mt-2">
                        <v-btn icon class="me-2" href="#" target="_blank">
                            <v-icon>mdi-facebook</v-icon>
                        </v-btn>
                        <v-btn icon class="me-2" href="#" target="_blank">
                            <v-icon>mdi-twitter</v-icon>
                        </v-btn>
                        <v-btn icon href="#" target="_blank">
                            <v-icon>mdi-linkedin</v-icon>
                        </v-btn>
                    </div>
                </v-col>
            </v-row>

            <v-divider class="my-4"></v-divider>

            <!-- Copyright -->
            <v-row>
                <v-col class="text-center">
                    <p class="text-body-2">&copy; {{ new Date().getFullYear() }} YenHost. All rights reserved.</p>
                </v-col>
            </v-row>
        </v-container>
    </v-footer>
</template>

<script setup>
import mainLogo from '@/assets/logo.png';

const footerLinks = [
    { title: 'cPanel Hosting', link: '/hosting/cpanel' },
    { title: 'WordPress Hosting', link: '/hosting/wordpress' },
    { title: 'Domains', link: '/domain/registration' },
    { title: 'Pricing', link: '/pricing' },
    { title: 'Contact', link: '/contact' },
];
</script>
