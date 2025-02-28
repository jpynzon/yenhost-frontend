<template>
    <page-content title="Get in Touch with Us" subtitle="We're Here to Help"
        description="Have questions or need assistance? Our team is ready to support you. Reach out to us and let's connect."
        :features="[
            { icon: 'mdi-email', text: 'support@yenhost.com' },
            { icon: 'mdi-facebook', text: 'YenHost', link: 'https://facebook.com/yenhostofficial' }
        ]" benefitsTitle="Send us a message" :benefits="[
            'We prioritize customer satisfaction and aim to provide the best support experience.',
            'Our dedicated team is available to assist you with any inquiries or technical support.',
            'Whether it’s a general question or a specific issue, we’re here to help!'
        ]" :image="contactImage" :backgroundImage="contactPreview" backgroundCss="center" />
</template>

<script setup>
// import contactImage from '@/assets/images/customer-support-illustration.png';
import contactPreview from '@/assets/images/contact.jpg';
</script>
