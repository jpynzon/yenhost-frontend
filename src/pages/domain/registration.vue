<template>
    <page-content title="Register Your Perfect Domain" subtitle="Secure Your Online Identity"
        description="Claim your unique domain name and establish a strong online presence. Whether for business or personal use, a custom domain gives you credibility and control over your brand."
        :features="[
            { icon: 'mdi-earth', text: 'Choose from a wide range of domain extensions' },
            { icon: 'mdi-lock-check', text: 'Secure domain privacy and protection' },
            { icon: 'mdi-speedometer', text: 'Fast registration and easy domain management' }
        ]" benefitsTitle="Why Register Your Domain With Us?" :benefits="[
            'A domain name is your digital identity. Our hassle-free registration process ensures you get the perfect name for your website, blog, or business.',
            'Enjoy competitive pricing, domain privacy protection, and seamless integration with our hosting solutions.',
            'Take the first step in establishing your online brand today!'
        ]" :image="domainImage" :backgroundImage="domainPreview" />
</template>

<script setup>
// import domainImage from '@/assets/images/domain-registration.webp';
import domainPreview from '@/assets/images/domain.jpg';
</script>