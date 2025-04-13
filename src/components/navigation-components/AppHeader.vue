<template>
    <div class="bg-primary">
        <v-app-bar elevation="0">
            <v-container class="d-flex align-center" fluid>
                <v-card to="/" height="100%" max-height="50px" min-width="150px" variant="text">
                    <v-img :src="mainLogo" height="100%" width="100%" />
                </v-card>

                <v-spacer />

                <div v-for="item in navLink" :key="item.title" class="hidden-sm-and-down">
                    <v-menu v-if="item.menuType">
                        <template v-slot:activator="{ props }">
                            <v-btn v-bind="props" height="50px" class="px-5" rounded="lg">
                                {{ item.title }} <v-icon>mdi-chevron-down</v-icon>
                            </v-btn>
                        </template>
                        <v-list class="rounded-lg">
                            <v-list-item v-for="submenu in item.menu" :key="submenu.title" class="text-primary"
                            :to="submenu.href ? undefined : submenu.link" @click="handleClick(submenu)">
                            <v-list-item-title>{{ submenu.title }}</v-list-item-title>
                        </v-list-item>
                        </v-list>
                    </v-menu>

                    <v-btn v-else :to="item.link" height="50px" class="px-5" rounded="lg">
                        {{ item.title }}
                    </v-btn>
                </div>

                <v-spacer />

                <v-btn class="me-3 hidden-md-and-up" icon="mdi-menu" @click.stop="toggleSidebar" />
                <div class="hidden-sm-and-down">
                    <v-btn @click="goToLoginPage" height="50px" class="px-5 me-3" variant="outlined" color="primary"
                        rounded="lg">Login</v-btn>
                    <v-btn @click="goToRegisterPage" append-icon="mdi-arrow-right" height="50px" class="px-8 bg-primary"
                        rounded="lg">Register</v-btn>
                </div>
            </v-container>
        </v-app-bar>

        <v-navigation-drawer v-if="sidebar" v-model="sidebar" location="right" temporary>
            <v-list>
                <div v-for="item in navLink" :key="item.title">
                    <v-list-group v-if="item.menuType" :value="item.title">
                        <template v-slot:activator="{ props }">
                            <v-list-item v-bind="props">
                                <v-list-item-title>{{ item.title }}</v-list-item-title>
                            </v-list-item>
                        </template>
                        <v-list-item v-for="submenu in item.menu" :key="submenu.title"
                            :to="submenu.href ? undefined : submenu.link" @click="handleClick(submenu)">
                            <v-list-item-title>{{ submenu.title }}</v-list-item-title>
                        </v-list-item>
                    </v-list-group>

                    <v-list-item v-else :to="item.link">
                        <v-list-item-title>{{ item.title }}</v-list-item-title>
                    </v-list-item>
                </div>

                <v-col>
                    <v-btn @click="goToLoginPage" height="50px" class="px-5 mb-3 w-100" variant="outlined"
                        color="primary" rounded="lg">Login</v-btn>
                    <v-btn @click="goToRegisterPage" append-icon="mdi-arrow-right" height="50px"
                        class="px-8 bg-primary w-100" rounded="lg">Register</v-btn>
                </v-col>
            </v-list>
        </v-navigation-drawer>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import { goToLoginPage, goToRegisterPage } from '@/utils.js';
import mainLogo from '@/assets/logo.png';

const sidebar = ref(false);

const toggleSidebar = () => {
    sidebar.value = !sidebar.value;
};

const navLink = [
    {
        title: 'Hosting', link: '/', menuType: true,
        menu: [
            { title: 'Shared Hosting', href: 'https://my.yenhost.com/order.php?step=1&productGroup=1' },
            /* { title: 'WordPress Hosting', link: '/hosting/wordpress' }, */
            /* { title: 'Professional Email', link: '/professional-email' }, */
        ]
    },
    {
        title: 'Domain', link: '/', menuType: true,
        menu: [
            { title: 'Domain Registration', link: null, href: 'https://my.yenhost.com/order.php?step=1&productGroup=2' },
            // { title: 'Domain Transfer', link: '/domain/transfer' },
        ]
    },
    // { title: 'Pricing', link: '/pricing', menuType: false },
    // { title: 'Contact', link: '/contact', menuType: false },
];

const handleClick = (submenu) => {
    if (submenu.href) {
        window.location.href = submenu.href;
    }
};
</script>