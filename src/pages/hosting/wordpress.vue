<template>
    <page-content title="WordPress Hosting" subtitle="The #1 Website Builder"
        description="Power your website with the world's most popular website builder. Enjoy lightning-fast performance, robust security, and seamless management."
        :features="[
            { icon: 'mdi-speedometer', text: 'Optimized for speed and reliability' },
            { icon: 'mdi-shield-check', text: 'Advanced security to protect your site' },
            { icon: 'mdi-tools', text: 'One-click installation & easy management' }
        ]" benefitsTitle="What is WordPress Toolkit?" :benefits="[
            'WordPress Toolkit is a comprehensive management interface available in cPanel that makes it easy to install, configure, and manage your WordPress websites.',
            'With WordPress Toolkit, managing your WordPress websites has become more convenient than ever before.',
            'It includes staging, cloning, syncing, updating, copying, and more.'
        ]" :image="wordpressToolkitImage" :backgroundImage="wordpressHostingPreview" />
</template>

<script setup>
import wordpressToolkitImage from '@/assets/images/wordpresstoolkit.webp';
import wordpressHostingPreview from '@/assets/images/wordpress-hosting.webp';
</script>
