<template>
    <page-content title="cPanel Hosting" subtitle="The #1 Hosting Control Panel"
        description="Manage your website with ease using cPanel – the industry's leading hosting control panel. Enjoy powerful tools, seamless website management, and top-notch security."
        :features="[
            { icon: 'mdi-speedometer', text: 'High-speed performance and 99.9% uptime' },
            { icon: 'mdi-lock', text: 'Robust security features & free SSL' },
            { icon: 'mdi-application', text: 'One-click app installations with Softaculous' }
        ]" benefitsTitle="Why Choose cPanel Hosting?" :benefits="[
            'cPanel simplifies website and server management with an intuitive interface and powerful tools.',
            'Whether you\'re a beginner or an expert, cPanel provides everything you need to manage your hosting efficiently.',
            'With cPanel, you can manage domains, email accounts, databases, and more with just a few clicks. Easily install applications, secure your site, and monitor your server performance all in one place.'
        ]" :image="cpanelImage" :backgroundImage="cpanelPreview" />
</template>

<script setup>
import cpanelImage from '@/assets/images/cpanel-dashboard.webp';
import cpanelPreview from '@/assets/images/cpanel-dashboard.webp';
</script>
