<template>
  <div class="energy-healing no-page-padding">
    <div v-if="data.banner">
      <SiteBannerFixed :imgUrl="data.banner.url" />
    </div>

    <div class="layout-image-text about">
      <div class="text-wrapper">
        <div class="text-wrapper-inner">
          <h1 v-if="data.about.title" class="heading-style">
            POWER UP Your Mind, Body, and Spirit: How to Live a Self-Loving Lifestyle
          </h1>
        </div>
      </div>

      <div class="text-wrapper">
        <div class="text-wrapper-inner">
          <p v-if="data.about.textLarge" class="large-text-style mb-24">
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

    <div class="layout-image-text">
      <div class="text-wrapper">
        <div class="text-wrapper-inner">
          <h2 v-if="data.system.title" class="title-style">
            {{ data.system.title }}
          </h2>
          <div v-if="data.system.text" class="rte">
            <SanityContent :blocks="data.system.text" />
          </div>
        </div>
      </div>

      <div class="image-wrapper">
        <figure v-if="data.system.img">
          <img
            :src="$urlFor(data.system.img.url).width(1200).auto('format')"
            :alt="data.system.img.alt"
          />
        </figure>
      </div>
    </div>

    <div class="layout-image-text techniques">
      <div class="image-wrapper">
        <figure v-if="data.techniques.img">
          <img
            :src="$urlFor(data.techniques.img.url).width(1200).auto('format')"
            :alt="data.techniques.img.alt"
          />
        </figure>
      </div>
      <div class="text-wrapper">
        <div class="text-wrapper-inner">
          <h2 v-if="data.techniques.title" class="title-style">
            {{ data.techniques.title }}
          </h2>
          <div v-if="data.techniques.text" class="rte">
            <SanityContent :blocks="data.techniques.text" />
          </div>
        </div>
      </div>
    </div>
    <div v-if="data.cta">
      <SiteCTA :data="data.cta" />
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
`;

export default {
  head() {
    return {
      title: "What is Energy Healing",
    };
  },
  async asyncData({ $sanity }) {
    const data = await $sanity.fetch(query).then((res) => res);
    return { data };
  },
};
</script>

<style lang="scss">
.energy-healing {
  .layout-image-text {
    // grid-template-rows: 50vw;
    .text-wrapper {
      @media (min-width: $collapse-bp) {
        padding: 44px 16px;
      }
    }
    h2 {
      @media (min-width: $collapse-bp) {
        margin-bottom: 44px;
      }
      @media (max-width: $collapse-bp) {
        margin-bottom: 24px;
      }
    }
  }

  .about {
    grid-template-rows: auto;
    > *:first-child {
      align-self: start;
    }
    > *:last-child {
      @media (min-width: $collapse-bp) {
        padding-top: 70px;
      }
    }
  }
  .techniques {
    ul {
      list-style: none;
      li:before {
        content: "*";
        margin-right: 1ch;
      }
    }
  }
}
</style>
