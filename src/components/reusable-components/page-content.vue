<template>
    <v-container>
        <v-col cols="12">
            <v-card variant="text" class="py-10">
                <v-row>
                    <v-col cols="12" md="6">
                        <h2 class="text-subtitle-2 mb-2">{{ subtitle }}</h2>
                        <h1 class="text-h5 font-weight-bold mb-5">{{ title }}</h1>
                        <p class="text-body-1 mb-5">{{ description }}</p>

                        <div v-for="(feature, index) in features" :key="index" class="d-flex align-center my-3">
                            <span class="me-2">
                                <v-icon>{{ feature.icon }}</v-icon>
                            </span>
                            <p class="text-body-2" :class="{ 'cursor-pointer text-primary': feature.link }"
                                @click="goToFeature(feature.link)">{{
                                    feature.text }}</p>
                        </div>

                        <v-btn v-if="actionButtonLabel" color="primary" class="mt-5" height="50px" rounded="lg"
                            :href="actionButtonLink">{{
                                actionButtonLabel }}</v-btn>
                    </v-col>

                    <v-col cols="12" md="6">
                        <v-card height="100%" width="700px" class="card-image" elevation="5" rounded="t-xl"
                            :style="{ backgroundImage: `url(${backgroundImage})`, backgroundPosition: backgroundCss }" />
                    </v-col>
                </v-row>
            </v-card>
        </v-col>

        <div class="py-15">
            <pricing-section />
        </div>

        <div class="page-title mb-10 text-center">
            <h1 class="text-h4 font-weight-bold mb-5">{{ benefitsTitle }}</h1>
            <h1 v-for="(benefit, index) in benefits" :key="index" class="text-subtitle-1 mb-5">
                {{ benefit }}
            </h1>

            <v-col cols="10" class="mx-auto">
                <v-img :src="image" rounded="xl"></v-img>
            </v-col>
        </div>
    </v-container>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    title: String,
    subtitle: String,
    description: String,
    features: Array, // [{ icon: 'mdi-email', text: 'Feature description' }]
    benefitsTitle: String,
    benefits: Array, // List of benefits
    image: String,
    backgroundImage: String,
    backgroundCss: String,
    actionButtonLabel: String,
    actionButtonLink: String
});

const goToFeature = (link) => {
    if (link) {
        window.open(link, '_blank');
    }
};
</script>

<style scoped>
.card-image {
    bottom: -40px;
    right: -50px;
    background-position: top left;
    background-size: cover;
}
</style>