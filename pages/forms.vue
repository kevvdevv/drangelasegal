<template>
  <div class="text-center page-container newsletter-page">
    <div class="page-title">
      <div class="text-wrapper">
        <div class="text-wrapper-inner">
          <h2>{{ data.header }}</h2>
          <ul style="list-style-type: none;">
            <li v-for="(formItem) in data.formList">
              <a :href="`${formItem.url}`">
                {{ formItem.title }}
              </a>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
  import { groq } from "@nuxtjs/sanity";
  import { ref } from 'vue';
  const query = groq`
    *[_type in ["clientForm"]] [0]
    `;
  export default {
    head() {
      return {
        title: "Forms",
      };
    },
  async asyncData({ $sanity }) {
    const data = await $sanity.fetch(query).then((res) => res);
    return { data };
  },
};
</script>