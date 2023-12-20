<template>
  <div class="index-page no-page-padding">
    <div class="aweber-form">
      <HomeAweberForm />
    </div>
    <div class="home-banner-container">
      <div v-if="data.banner">
        <HomeBanner :data="data.banner" />
      </div>
    </div>
    <div v-if="data.power_up">
      <HomePowerUp :data="data.power_up" />
    </div>
    <div class="homepage-video-wrapper">
      <client-only>
        <vimeo-player ref="player" :video-id="videoID" @ready="onReady" :player-height="height"/>
      </client-only>
    </div>
    <!-- <div class="flex-row">
      <div v-if="data.callout_left">
        <HomeCallout :data="data.callout_left" />
      </div>
      <div v-if="data.callout_right">
        <HomeCallout :data="data.callout_right" />
      </div>
    </div> -->
    <div v-if="data.testimonial">
      <HomeTestimonial :data="data.testimonial" />
    </div>
  </div>
</template>

<script>
import { groq } from "@nuxtjs/sanity";
const query = groq`
*[_type in ["home"]][0]{
  "banner": {
    "img1": {
      "url": banner.img1.image.asset->url,
      "alt": banner.img1.image.asset->altText
    },
    "img2": {
      "url": banner.img2.image.asset->url,
      "alt": banner.img2.image.asset->altText
    },
    "img3": {
      "url": banner.img3.image.asset->url,
      "alt": banner.img3.image.asset->altText
    },
  },
  "power_up":  {
    "text": power_up,
    "hasNewsletter": addForm,
    "newsletter": power_up_newsletter
  },
  "callout_left": {
    "img": {
      "url": callout_left.img.image.asset->url,
      "alt": callout_left.img.image.asset->altText
    },
    "title": callout_left.title,
    "button": callout_left.button
  },
  "callout_right": {
    "img": {
      "url": callout_right.img.image.asset->url,
      "alt": callout_right.img.image.asset->altText
    },
    "title": callout_right.title,
    "button": callout_right.button
  },
  "testimonial": {
    "img": {
      "url": testimonial.img.image.asset->url,
      "alt": testimonial.img.image.asset->altText
    },
     "quote": testimonial.testimonial->quote,
     "name": testimonial.testimonial->name,
  }
}
`;

export default {
  head() {
    return {
      title: "Home",
    };
  },
  async asyncData({ $sanity }) {
    const data = await $sanity.fetch(query).then((res) => res);
    return { data };
  },
  data() {
		return {
			videoID: '894621415',
			height: 500,
			options: {
				muted: true,
	      			autoplay: true,
			},
			playerReady: false
		}
	},
	methods: {
		onReady() {
			this.playerReady = true
		},
		play () {
			this.$refs.player.play()
		},
		pause () {
			this.$refs.player.pause()
		}
	}
};
</script>

<style lang="scss">
.home-banner-container {
  background: $sand;
  height: calc(100vh - $headerHeight);
  max-height: calc(100vh - $headerHeight);
  overflow: hidden;

  >div {
    height: 100%;
  }
}
.homepage-video-wrapper {
    position: relative;
    padding-bottom: 56.25%; /* 16:9 */
    padding-top: 25px;
    height: 0;
}
.homepage-video-wrapper iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
}
</style>
