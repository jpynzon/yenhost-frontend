<template>
    <v-container>
        <div class="page-title mb-10 text-center">
            <h1 class="text-h4 font-weight-bold">FAQ</h1>
        </div>

        <v-col cols="12">
            <v-expansion-panels v-model="activePanel" variant="popout" rounded="xl">
                <v-expansion-panel v-for="(item, index) in faqs" :key="item.question"
                    :class="{ 'text-primary': activePanel === index }">
                    <v-expansion-panel-title>
                        <h1 class="text-body-1 font-weight-bold py-2">
                            {{ item.question }}
                        </h1>
                    </v-expansion-panel-title>
                    <v-expansion-panel-text class="bg-grey-lighten-3 rounded-b-xl">
                        <p class="py-5 text-body-2">
                            {{ item.answer }}
                        </p>
                    </v-expansion-panel-text>
                </v-expansion-panel>
            </v-expansion-panels>
        </v-col>
    </v-container>
</template>

<script setup>
import { ref } from "vue";

const activePanel = ref(0);

const faqs = [
    {
        question: "What is Web Hosting and how does it work?",
        answer: "Web hosting is simply offering storage space for any application or website on special computers called servers, which allows individuals or companies to create and post a website. Once a website is hosted or stored on a server, users can simply access it by typing the domain name (web address) in their browser."
    },
    {
        question: "Can I use your web hosting service even I have zero technical knowledge?",
        answer: "Yes, our service can cater to novice or non-technical individuals to create websites easily. Our provider offers an application called Installatron that provides multiple free web applications via one-click installation. Our web hosting services are user- friendly and offer over 100 free web applications.These applications span a wide range of functionalities, including content management, community building, e - commerce, statistics, and surveys.Our selection includes popular apps such as WordPress, Joomla, Drupal, Magento, and more!"
    },
    {
        question: "Is my personal data safe?",
        answer: "Yes, we follow strict security protocols to ensure your personal data is protected and never shared with third parties."
    },
    {
        question: "What services do you provide?",
        answer: "We offer web hosting with Softaculous installer, WordPress, personalized email, and domain services."
    },
    {
        question: "How do I report a technical issue?",
        answer: "You can report technical issues by submitting a detailed message through our contact form or emailing our support team."
    },
];
</script>
