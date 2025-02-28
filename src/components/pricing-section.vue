<template>
    <v-container>
        <div class="page-title mb-10 text-center">
            <h1 class="text-h4 font-weight-bold">Flexible Pricing Plans</h1>
            <h1 class="text-subtitle-1">
                Choose a plan that fits your needs and budget—no hidden fees, just premium value.
            </h1>
        </div>

        <div class="d-flex flex-wrap justify-space-between align-center">
            <!-- Billing Toggle -->
            <v-card class="d-flex align-center mb-5" rounded="lg">
                <v-card class="px-5 py-1 cursor-pointer" :class="{ 'bg-primary text-white': !isYearly }" rounded="0"
                    @click="isYearly = false" :variant="isYearly ? 'flat' : 'text'">
                    Monthly
                </v-card>
                <v-card class="px-5 py-1 cursor-pointer" :class="{ 'bg-primary text-white': isYearly }" rounded="0"
                    @click="isYearly = true" :variant="isYearly ? 'flat' : 'text'">
                    Yearly
                </v-card>
            </v-card>

            <!-- Currency Selector -->
            <div class="mb-5">
                <span class="text-subtitle-2 me-3">Choose your currency:</span>
                <v-btn rounded="lg">
                    {{ selectedCurrency.title }}
                    <v-icon>mdi-chevron-down</v-icon>
                    <v-menu activator="parent">
                        <v-list>
                            <v-list-item v-for="(currency, index) in currencies" :key="index"
                                @click="changeCurrency(currency)">
                                <v-list-item-title>{{ currency.title }}</v-list-item-title>
                            </v-list-item>
                        </v-list>
                    </v-menu>
                </v-btn>
            </div>
        </div>

        <v-row>
            <v-col v-for="(plan, index) in displayedPricings" :key="index" cols="12" md="4">
                <v-card :class="{ 'bg-primary px-1 py-1': plan.mostPopular }" rounded="xl" elevation="3">
                    <h1 v-if="plan.mostPopular" class="text-subtitle-1 text-center">Most Popular</h1>

                    <v-card class="px-5 py-10" rounded="xl">
                        <div class="title mb-5">
                            <h1 class="text-h6">{{ plan.title }}</h1>
                            <h1 class="text-subtitle-2">{{ plan.subtitle }}</h1>
                        </div>

                        <div class="price mb-5">
                            <h1 class="text-h3 font-weight-bold">
                                <span class="text-h6">{{ selectedCurrency.symbol }}</span>
                                {{ convertPrice(plan.price) }}
                                <span class="text-h6">/{{ isYearly ? 'yr' : 'mo' }}</span>
                            </h1>
                        </div>

                        <v-btn @click="goToRegisterPage" height="50px" color="primary" rounded="lg" class="w-100">Choose
                            plan</v-btn>

                        <v-divider class="mt-5 mb-10" />

                        <div class="features">
                            <p v-for="(feature, i) in plan.features" :key="i" class="text-body-1">
                                <v-icon class="me-2 text-success">mdi-check</v-icon>{{ feature }}
                            </p>
                        </div>
                    </v-card>
                </v-card>
            </v-col>
        </v-row>
    </v-container>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';
import { goToLoginPage, goToRegisterPage } from '@/utils.js';

const pricings = [
    {
        mostPopular: false,
        title: 'Starter',
        subtitle: 'Perfect for a single website',
        price: 171,
        features: [
            '10 GB SSD Storage',
            'Unlimited Websites',
            'Unlimited Email & DB',
            'Unmetered Bandwidth',
            'Imunify 360 Security Protection',
            'Free Automated Backups',
            'Free 1-Click Auto Installer',
            'Free Domain Name']
    },
    {
        mostPopular: true,
        title: 'Personal',
        subtitle: 'Ideal for personal website',
        price: 316,
        features: [
            '50 GB SSD Storage',
            'Unlimited Websites',
            'Unlimited Email & DB',
            'Unmetered Bandwidth',
            'Imunify 360 Security Protection',
            'Free Automated Backups',
            'Free 1-Click Auto Installer',
            'Free Domain Name']
    },
    {
        mostPopular: false,
        title: 'Business',
        subtitle: 'For businesses with high traffic',
        price: 578,
        features: [
            '100 GB SSD Storage',
            'Unlimited Websites',
            'Unlimited Email & DB',
            'Unmetered Bandwidth',
            'Imunify 360 Security Protection',
            'Free Automated Backups',
            'Free 1-Click Auto Installer',
            'Free Domain Name']
    }
];

// Currency options
const currencies = [
    { title: 'Philippines (₱)', symbol: '₱', rate: 1 },
    { title: 'United States ($)', symbol: 'US$', rate: 1 / 53 },
    { title: 'Euro (€)', symbol: '€', rate: 1 / 58 },
];

const isYearly = ref(false);
const selectedCurrency = ref(currencies[0]); // Default currency: PHP

// Load currency from localStorage
onMounted(() => {
    const savedCurrency = localStorage.getItem('currency');
    if (savedCurrency) {
        selectedCurrency.value = JSON.parse(savedCurrency);
    }
});

// Change currency and save to localStorage
const changeCurrency = (currency) => {
    selectedCurrency.value = currency;
    localStorage.setItem('currency', JSON.stringify(currency));
};

// Compute the displayed prices
const displayedPricings = computed(() => {
    return pricings.map(plan => ({
        ...plan,
        price: isYearly.value ? plan.price * 12 * 0.85 : plan.price // 15% discount on yearly plans
    }));
});

// Convert price based on currency
const convertPrice = (price) => {
    return (price * selectedCurrency.value.rate).toFixed(2);
};
</script>

<style scoped>
.cursor-pointer {
    cursor: pointer;
}
</style>
