<template>
  <div
    class="
      container
      mx-auto
      flex
      items-center
      min-h-screen
      justify-center
      px-3
      sm:px-0
    "
  >
    <div
      class="flex justify-center flex-col p-8 bg-gray-900"
      style="min-height: 400px"
    >
      <div class="flex justify-center text-gray-600">
        <nuxt-link
          v-for="locale in availableLocales"
          :key="locale.code"
          class="mr-3"
          :to="switchLocalePath(locale.code)"
          >{{ locale.name }}</nuxt-link
        >
      </div>
      <h1 class="text-3xl text-gray-200 sm:text-4xl pb-4 font-bold text-center">
        {{ $t('title') }}
      </h1>
      <div
        class="
          text-sm
          sm:text-lg
          text-gray-200 text-center
          flex flex-col
          justify-center
        "
      >
        <span class="max-w-screen-sm">
          {{ $t('info') }}
        </span>
        <!-- <a
          v-for="(item, index) in more"
          v-show="item.lang === $i18n.getLocaleCookie()"
          :key="index"
          :href="item.url"
          class="underline"
        >
          {{ $t('more') }}
        </a> -->
        <NuxtLink
          v-if="$i18n.getLocaleCookie() !== 'fi'"
          to="/form"
          class="pt-3 text-xl sm:text-4xl text-white underline"
        >
          {{ $t('apply') }}
        </NuxtLink>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      more: [
        {
          url: '/Festival Feast After Plague.pdf',
          lang: 'en',
        },
        {
          url: '/Pitkä versio suomeksi.pdf',
          lang: 'fi',
        },
        {
          url: '/Пир после чумы.pdf',
          lang: 'ru',
        },
      ],
    }
  },
  computed: {
    availableLocales() {
      return this.$i18n.locales.filter((i) => i.code !== this.$i18n.locale)
    },
  },
}
</script>
