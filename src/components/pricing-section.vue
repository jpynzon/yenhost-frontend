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
                    @click="isYearly = false">
                    Monthly
                </v-card>
                <v-card class="px-5 py-1 cursor-pointer" :class="{ 'bg-primary text-white': isYearly }" rounded="0"
                    @click="isYearly = true">
                    Yearly
                </v-card>
            </v-card>

            <!-- Currency Selector -->
            <div class="mb-5">
                <span class="text-subtitle-2 me-3">Choose your currency:</span>
                <v-menu>
                    <template v-slot:activator="{ props }">
                        <v-btn v-bind="props" rounded="lg">
                            {{ selectedCurrency.symbol }} {{ selectedCurrency.title }}
                            <v-icon>mdi-chevron-down</v-icon>
                        </v-btn>
                    </template>
                    <v-list>
                        <v-list-item v-for="currency in currencies" :key="currency.title"
                            @click="changeCurrency(currency)">
                            <v-list-item-title>
                                {{ currency.symbol }} {{ currency.title }}
                            </v-list-item-title>
                        </v-list-item>
                    </v-list>
                </v-menu>
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
                            <h1 class="text-h3 font-weight-bold mb-3">
                                <span class="text-h6">{{ selectedCurrency.symbol }}</span>
                                {{ convertPrice(plan.price) }}
                                <span class="text-h6">/{{ isYearly ? 'yr' : 'mo' }}</span>
                            </h1>
                        </div>

                        <v-btn :href="plan.link" height="50px" color="primary" rounded="lg" class="w-100">Choose
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
import axios from 'axios';

const isYearly = ref(false);
const selectedCurrency = ref({ title: 'Philippines', symbol: '₱', rate: 1 });

const currencies = ref([
    { title: 'Philippines', symbol: '₱', rate: 1 },
    { title: 'USD', symbol: '$', rate: 0.01724 }
]);

// Fetch USD rate dynamically
const fetchExchangeRate = async () => {
    try {
        const response = await axios.get("https://v6.exchangerate-api.com/v6/b61e6230e191adc218b45088/latest/PHP");
        if (response.data.result === "success") {
            // Update the exchange rate dynamically
            currencies.value = currencies.value.map(currency =>
                currency.title === "USD" ? { ...currency, rate: response.data.conversion_rates.USD } : currency
            );
        }
    } catch (error) {
        console.error("Failed to fetch exchange rate:", error);
    }
};

onMounted(() => {
    fetchExchangeRate();
    const savedCurrency = localStorage.getItem('currency');

    try {
        if (savedCurrency) {
            const parsedCurrency = JSON.parse(savedCurrency);
            // Check if parsedCurrency exists in the available currencies
            const foundCurrency = currencies.value.find(currency => currency.title === parsedCurrency.title);
            if (foundCurrency) {
                selectedCurrency.value = foundCurrency;
            } else {
                selectedCurrency.value = currencies.value[0]; // Default to PHP
            }
        } else {
            selectedCurrency.value = currencies.value[0]; // Default to PHP
        }
    } catch (error) {
        console.error("Error parsing currency from localStorage:", error);
        selectedCurrency.value = currencies.value[0]; // Fallback to PHP
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

        if (isYearly.value && plan.title !== 'Starter' && !updatedFeatures.includes('Free 1 Year Domain')) {
            updatedFeatures.push('Free 1 Year Domain');
        }

        return {
            ...plan,
            features: updatedFeatures,
            price: isYearly.value ? plan.price * 12 : plan.price
        };
    });
});

// Convert price based on currency and add commas
const convertPrice = (price) => {
    const rate = selectedCurrency.value.rate ?? 1; // Use 1 if undefined
    return (price * rate).toFixed(2).replace(/\d(?=(\d{3})+\.)/g, '$&,');
};


const pricings = [
    {
        mostPopular: false,
        title: 'Starter',
        subtitle: 'Perfect for a single website',
        price: 171,
        features: ['10 GB SSD Storage', '3 Websites', '100GB Bandwidth', '30 Mailboxes', 'Website Builder', 'Free SSL'],
        link: 'https://billing.yenhost.com/order?product=2'
    },
    {
        mostPopular: true,
        title: 'Personal',
        subtitle: 'Ideal for personal website',
        price: 316,
        features: ['20 GB SSD Storage', 'Unlimited Websites', 'Unlimited Mailboxes', 'Unmetered Bandwidth', 'Website Builder', 'Free SSL'],
        link: 'https://billing.yenhost.com/order?product=3'
    },
    {
        mostPopular: false,
        title: 'Business',
        subtitle: 'For businesses with high traffic',
        price: 578,
        features: ['50 GB SSD Storage', 'Unlimited Websites', 'Unlimited Mailboxes', 'Unmetered Bandwidth', 'Website Builder', 'Free SSL'],
        link: 'https://billing.yenhost.com/order?product=4'
    }
];

</script>

<style scoped>
.cursor-pointer {
    cursor: pointer;
}

.dashed-price {
    text-decoration: line-through;
}
</style>
