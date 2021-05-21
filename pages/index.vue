<template>
  <div
    class="
      container
      mx-auto
      flex
      items-center
      h-screen
      justify-center
      px-3
      sm:px-0
    "
  >
    <div
      class="flex justify-center flex-col border-4 border-white p-8 bg-gray-900"
    >
      <div class="flex justify-center text-gray-600">
        <nuxt-link
          v-for="locale in availableLocales"
          class="mr-3"
          :key="locale.code"
          :to="switchLocalePath(locale.code)"
          >{{ locale.name }}</nuxt-link
        >
      </div>
      <h1 class="text-3xl text-gray-200 sm:text-4xl pb-4 font-bold text-center">
        {{ $t('title') }}
      </h1>
      <div
        class="text-sm sm:text-lg text-gray-200 text-center flex justify-center"
      >
        <div class="max-w-screen-sm">
          {{ $t('info') }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  computed: {
    availableLocales() {
      return this.$i18n.locales.filter((i) => i.code !== this.$i18n.locale)
    },
  },
}
</script>
