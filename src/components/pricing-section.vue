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

                        <div v-if="isYearly" class="d-flex align-center mb-5">
                            <v-chip class="me-3">
                                <v-icon>mdi-percent</v-icon>
                                15 off
                            </v-chip>
                            <h1 class="text-subtitle-1 dashed-price">
                                <span>{{ selectedCurrency.symbol }}</span>
                                {{ convertPrice(plan.price * (isYearly ? 1 / 0.85 : 1)) }}
                            </h1>
                        </div>

                        <div class="price mb-5">
                            <h1 class="text-h3 font-weight-bold mb-3">
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
            '3 Websites',
            '100GB Bandwidth',
            '30 Mailboxes',
            'Website Builder',
            'Free SSL']
    },
    {
        mostPopular: true,
        title: 'Personal',
        subtitle: 'Ideal for personal website',
        price: 316,
        features: [
            '20 GB SSD Storage',
            'Unlimited Websites',
            'Unlimited Mailboxes',
            'Unmetered Bandwidth',
            'Website Builder',
            'Free SSL']
    },
    {
        mostPopular: false,
        title: 'Business',
        subtitle: 'For businesses with high traffic',
        price: 578,
        features: [
            '50 GB SSD Storage',
            'Unlimited Websites',
            'Unlimited Mailboxes',
            'Unmetered Bandwidth',
            'Webiste Builder',
            'Free SSL']
    }
];

// Currency options
const currencies = [
    { title: 'Philippines (₱)', symbol: '₱', rate: 1 },
    { title: 'United States ($)', symbol: 'US$', rate: 1 / 50 },
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
    return pricings.map(plan => {
        let updatedFeatures = [...plan.features];

        // Add "Free Domain Name" to ALL yearly plans (if not already included)
        if (isYearly.value && plan.title !== 'Starter' && !updatedFeatures.includes('Free 1 Year Domain')) {
            updatedFeatures.push('Free 1 Year Domain');
        }

        return {
            ...plan,
            features: updatedFeatures,
            price: isYearly.value ? plan.price * 12 * 0.85 : plan.price // 15% discount on yearly
        };
    });
});


// Convert price based on currency and add commas
const convertPrice = (price) => {
    return (price * selectedCurrency.value.rate)
        .toFixed(2)
        .replace(/\d(?=(\d{3})+\.)/g, '$&,'); // Add commas
};

</script>

<style scoped>
.cursor-pointer {
    cursor: pointer;
}

.dashed-price {
    text-decoration: line-through;
}
</style>
