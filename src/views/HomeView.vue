<template>
  <div class="home">
    <HeaderBeetwen />
    <HeroSection />
    <BannerSection />
    <InstaSection />
    <PartnerSection />
    <FooterSection />
  </div>
</template>

<script>
// @ is an alias to /src

import HeaderBeetwen from "@/components/HeaderBeetwen.vue";
import HeroSection from "@/components/HeroSection.vue";
import BannerSection from "@/components/BannerSection.vue";
import InstaSection from "@/components/Insta.vue";
import PartnerSection from "@/components/Partner.vue";
import FooterSection from "@/components/FooterSection.vue";

export default {
  name: "HomeView",
  components: {
    HeaderBeetwen,
    HeroSection,
    BannerSection,
    InstaSection,
    PartnerSection,
    FooterSection,
  },
};
</script>
