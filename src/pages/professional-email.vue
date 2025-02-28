<template>
    <page-content title="Personal Email with Webmail" subtitle="Your Professional Email Address"
        description="Create a custom email address like example@yourname.com and enhance your professional image."
        :features="[
            { icon: 'mdi-email', text: 'Send & receive emails with your domain-based address' },
            { icon: 'mdi-web', text: 'Access emails from anywhere using Webmail' },
            { icon: 'mdi-lock', text: 'Secure & private email hosting with spam protection' }
        ]" benefitsTitle="Why Choose Our Email Hosting?" :benefits="[
            'A personalized email address builds trust and credibility.',
            'Access from any device with an internet connection.',
            'Advanced spam filtering, calendar integration, and multi-device sync.'
        ]" :image="webmailImage" :backgroundImage="webmailPreview" />
</template>

<script setup>
import webmailImage from '@/assets/images/webmail-dashboard.webp';
import webmailPreview from '@/assets/images/webmail-preview.webp';
</script>
