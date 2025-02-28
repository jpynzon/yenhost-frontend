<template>
    <v-container>
        <div class="page-title mb-10 text-center">
            <h1 class="text-h4 font-weight-bold">Your Online Success Starts Here</h1>
            <h1 class="text-subtitle-1">
                Everything you need to launch, manage, and grow your online presence—effortlessly.
            </h1>
        </div>

        <v-col cols="12" v-for="item in products" :key="item.title">
            <v-card class="pa-10" rounded="xl" elevation="5" variant="tonal" color="primary">
                <v-row>
                    <v-col cols="12" md="6">
                        <h2 class="text-subtitle-2 mb-2">
                            {{ item.subtitle }}
                        </h2>
                        <h1 class="text-h5 font-weight-bold mb-5">
                            {{ item.title }}
                        </h1>
                        <p class="text-body-1">
                            {{ item.description }}
                        </p>
                    </v-col>

                    <v-col cols="12" md="6" class="d-flex flex-column justify-center">
                        <div class="d-flex align-center my-3" v-for="feature in item.features" :key="feature">
                            <span class="me-2 text-primary">
                                <v-icon>mdi-check-circle</v-icon>
                            </span>
                            <p class="text-body-2">
                                {{ feature }}
                            </p>
                        </div>
                    </v-col>
                </v-row>
            </v-card>
        </v-col>

        <!-- WordPress Section -->
        <v-col cols="12">
            <v-card class="pa-10" rounded="xl" color="primary-darken-1" elevation="5">
                <v-row>
                    <v-col cols="12" md="6">
                        <h2 class="text-subtitle-2 mb-2">The #1 Website Builder</h2>
                        <h1 class="text-h5 font-weight-bold mb-5">WordPress Hosting</h1>
                        <p class="text-body-1 mb-5">
                            Power your website with the world's most popular website builder.
                            Enjoy lightning-fast performance, robust security, and seamless management.
                        </p>

                        <div class="d-flex align-center my-3">
                            <span class="me-2">
                                <v-icon>mdi-speedometer</v-icon>
                            </span>
                            <p class="text-body-2">Optimized for speed and reliability</p>
                        </div>
                        <div class="d-flex align-center my-3">
                            <span class="me-2">
                                <v-icon>mdi-shield-check</v-icon>
                            </span>
                            <p class="text-body-2">Advanced security to protect your site</p>
                        </div>
                        <div class="d-flex align-center my-3">
                            <span class="me-2">
                                <v-icon>mdi-tools</v-icon>
                            </span>
                            <p class="text-body-2">One-click installation & easy management</p>
                        </div>
                    </v-col>

                    <v-col cols="12" md="6">
                        <v-card height="100%" width="1000px" class="card-image" elevation="5" rounded="lg" />
                    </v-col>
                </v-row>
            </v-card>
        </v-col>
    </v-container>
</template>

<script setup>
const products = [
    {
        title: 'Softaculous Installer',
        subtitle: 'Install 400+ applications with just a few clicks',
        description: 'Easily install, update, and manage over 400 applications, including WordPress, Joomla, and more. No technical knowledge required!',
        features: [
            'One-click setup for WordPress and other apps',
            'Access a library of 400+ powerful scripts',
            'Effortless updates to keep your software secure'
        ]
    }
];
</script>

<style scoped>
.card-image {
    bottom: -40px;
    right: -50px;
    background-image: url('@/assets/images/wordpress-hosting.webp');
    background-position: top left;
    background-size: cover;
}
</style>