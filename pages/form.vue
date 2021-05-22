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
        {{ $t('form.title') }}
      </h1>
      <form name="contact" netlify>
        <p>
          <label class="label">
            {{ $t('form.name') }} <input class="form" type="text" name="name"
          /></label>
        </p>
        <p>
          <label class="label">
            {{ $t('form.email') }}
            <input class="form" type="email" name="email"
          /></label>
        </p>
        <div class="text-center pt-4">
          <button
            class="text-white border border-white px-5 py-2 rounded"
            type="submit"
          >
            {{ $t('form.submit') }}
          </button>
        </div>
      </form>
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
