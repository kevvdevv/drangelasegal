<template>
  <div class="text-center page-container newsletter-page">
    <div class="layout-image-text about">
      <div class="text-wrapper">
        <div class="text-wrapper-inner">
          <h1 class="heading-style">
            POWER UP Your Mind, Body, and Spirit: How to Live a Self-Loving Lifestyle
          </h1>
        </div>
      </div>

      <div class="text-wrapper">
        <div class="text-wrapper-inner">
          <p class="large-text-style mb-24">
            A 7-Module Online Course Using Energy Medicine to Unlock Your Highest, Truest Self. In this powerful course, I'll walk you through the steps of how to begin a daily practice of deepening and increasing your Self-Loving living.
          </p>
          <p><a href="https://angelasegalphd.thinkific.com/courses/How-to-Live-a-Self-Loving-Lifestyle">More info on the course</a></p>
          <p><a href="https://angelasegalphd.thinkific.com/enroll/2189643?price_id=2951711">Register for the course</a></p>
          <p><a href="https://angelasegalphd.thinkific.com/enroll/2189643?price_id=3991900">Register for the course with flexible payment options</a></p>
          <div v-if="data.about.textMain" class="rte">
            <SanityContent :blocks="data.about.textMain" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { groq } from "@nuxtjs/sanity";
const query = groq`
     *[_type in ["energyHealing"]]{
 "about": {
    "title": about.title,
    "textLarge": about.text_large,
    "textMain": about.text.rte
  },
  "system": {
    "title": system.title,
    "text": system.text.rte,
    "img": {
      "url": system.img.image.asset->url,
      "alt": system.img.image.asset->altText
    }
  },
  "banner": {
      "url": banner.img.image.asset->url,
      "alt": banner.img.image.asset->altText
  },
  "cta": {
    "heading": cta.heading,
    "link": cta.link
}
}[0]
     *[_type in ["energyHealing"]]{
 "about": {
    "title": about.title,
    "textLarge": about.text_large,
    "textMain": about.text.rte
  },
  "system": {
    "title": system.title,
    "text": system.text.rte,
    "img": {
      "url": system.img.image.asset->url,
      "alt": system.img.image.asset->altText
    }
  },
  "banner": {
      "url": banner.img.image.asset->url,
      "alt": banner.img.image.asset->altText
  },
  "cta": {
    "heading": cta.heading,
    "link": cta.link
}
}[0]
   `;

export default {
  head() {
    return {
      title: "Newsletter",
    };
  },
  async asyncData({ $sanity }) {
    const data = await $sanity.fetch(query).then((res) => res);
    return { data };
  }
};
</script>
<style lang="scss">
@media (max-width: $collapse-bp) {
  .newsletter-page .newsletter-form {
    padding: 0 24px;
  }

  .newsletter-page .newsletter-form h2 {
    text-align: center;
    max-width: 100%;
  }
}
</style>