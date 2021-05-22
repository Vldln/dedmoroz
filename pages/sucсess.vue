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
        {{ $t('form.sucess') }}
      </h1>
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
