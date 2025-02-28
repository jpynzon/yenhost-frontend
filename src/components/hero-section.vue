<template>
    <v-container>
        <v-row class="d-flex align-center">
            <v-col cols="12" md="4">
                <h1 class="text-h4 font-weight-bold">
                    Bring Your Website to Life—Effortlessly
                </h1>
                <h1 class="text-h6 mb-5">
                    Get a <strong>free domain for a year</strong> when you choose an annual plan.
                </h1>
                <div class="checks mb-10">
                    <p v-for="item in offers" :key="item.title" class="text-body-1">
                        <v-icon class="me-2 text-success">{{ item.icon }}</v-icon>{{ item.title }}
                    </p>
                </div>
                <div class="action-buttons">
                    <v-btn @click="goToRegisterPage" class="px-10 w-100" height="50px" color="primary"
                        rounded="lg">Claim deal</v-btn>
                    <!-- <v-btn class="me-3 px-10" height="50px" color="primary" rounded="lg">Claim deal</v-btn>
                    <v-btn class="me-3 px-5" height="50px" color="primary" variant="tonal" rounded="lg">
                        {{ formattedTime }}
                    </v-btn> -->
                </div>
            </v-col>

            <v-col cols="12" md="8">
                <v-card height="100%" width="100%" variant="text">
                    <v-img :src="heroImage" height="100%" width="100%" cover />
                </v-card>
            </v-col>
        </v-row>
    </v-container>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import heroImage from '@/assets/images/hero-image.png';
import { goToLoginPage, goToRegisterPage } from '@/utils.js';

const offers = [
    { title: 'Free Domain', icon: 'mdi-check' },
    { title: 'Free SSL', icon: 'mdi-check' },
    { title: 'Website Builder', icon: 'mdi-check' },
    { title: 'Personalized Email', icon: 'mdi-check' },
    { title: '24/7 Customer Support', icon: 'mdi-check' }
];

const formattedTime = ref('00:00:00:00');
let countdownInterval = null;

const initializeCountdown = () => {
    const storedEndTime = localStorage.getItem('countdownEndTime');
    let endTime;

    if (storedEndTime) {
        endTime = parseInt(storedEndTime, 10);
    } else {
        const duration =
            (24 * 24 * 60 * 60 * 1000) +  // 24 days
            (18 * 60 * 60 * 1000) +       // 18 hours
            (33 * 60 * 1000) +           // 33 minutes
            (12 * 1000);                 // 12 seconds

        endTime = Date.now() + duration;
        localStorage.setItem('countdownEndTime', endTime);
    }

    updateCountdown(endTime);
    countdownInterval = setInterval(() => updateCountdown(endTime), 1000);
};

const updateCountdown = (endTime) => {
    const now = Date.now();
    const remainingTime = endTime - now;

    if (remainingTime <= 0) {
        formattedTime.value = '00:00:00:00';
        clearInterval(countdownInterval);
        localStorage.removeItem('countdownEndTime');
        return;
    }

    const days = Math.floor(remainingTime / (1000 * 60 * 60 * 24));
    const hours = Math.floor((remainingTime / (1000 * 60 * 60)) % 24);
    const minutes = Math.floor((remainingTime / (1000 * 60)) % 60);
    const seconds = Math.floor((remainingTime / 1000) % 60);

    formattedTime.value = `${String(days).padStart(2, '0')}:${String(hours).padStart(2, '0')}:${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}`;
};

onMounted(() => {
    initializeCountdown();
});

onUnmounted(() => {
    clearInterval(countdownInterval);
});
</script>
