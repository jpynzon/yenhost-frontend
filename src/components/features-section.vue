<template>
    <v-container>
        <div class="page-title mb-10 text-center">
            <h1 class="text-h4 font-weight-bold">Unlock Premium Features</h1>
            <h1 class="text-subtitle-1">Powerful tools designed to elevate your online presence and business growth.
            </h1>
        </div>

        <v-row>
            <v-col cols="12" md="4" v-for="item in features" :key="item.title">
                <v-card class="glass-card pa-5 h-100" rounded="xl">
                    <div class="card-title d-flex align-center mb-5">
                        <span class="icon-wrapper me-2">
                            <v-icon size="28">{{ item.icon }}</v-icon>
                        </span>
                        <h2 class="text-h6 font-weight-bold">{{ item.title }}</h2>
                    </div>
                    <div class="description">
                        <p class="text-body-1">
                            {{ item.description }}
                        </p>
                    </div>
                </v-card>
            </v-col>
        </v-row>
    </v-container>
</template>

<script setup>
const features = [
    {
        title: 'Free Domain',
        description: 'Claim your brand identity! Get a free domain for 1 year with any of our Annual Web Hosting Plans.',
        icon: 'mdi-web'
    },
    {
        title: 'Unmetered Bandwidth',
        description: "Your growth shouldn't be limited. Enjoy unlimited bandwidth and scale without extra costs.",
        icon: 'mdi-speedometer'
    },
    {
        title: 'Website Security',
        description: 'Win customer trust with our free SSL Certificate—because security means more conversions.',
        icon: 'mdi-shield-lock-outline'
    },
    {
        title: 'Reliable Email Service',
        description: 'Look professional! Create custom email addresses with your business domain and access them anywhere.',
        icon: 'mdi-email-outline'
    },
    {
        title: 'Website Backup',
        description: 'Always backup your files manually to make sure it is always up to date for recovery.',
        icon: 'mdi-cloud-upload-outline'
    },
    {
        title: 'Intuitive cPanel',
        description: 'Manage your hosting effortlessly with our user-friendly cPanel—no tech skills required!',
        icon: 'mdi-cog-outline'
    }
];
</script>

<style scoped>
/* Glassmorphic Effect */
.glass-card {
    background: rgba(255, 255, 255, 0.8);
    backdrop-filter: blur(10px);
    border: 1px solid rgba(255, 255, 255, 0.2);
    box-shadow: 0px 8px 32px rgba(0, 0, 0, 0.15);
    transition: all 0.3s ease;
}

.glass-card:hover {
    transform: scale(1.05);
}

/* Icon Background */
.icon-wrapper {
    background: rgba(255, 255, 255, 0.1);
    backdrop-filter: blur(5px);
    padding: 10px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
}
</style>
