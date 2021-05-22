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
      <form
        name="Apply"
        method="post"
        data-netlify="true"
        data-netlify-honeypot="bot-field"
      >
        <input type="hidden" name="form-name" value="ask-question" />
        <label class="label">
          {{ $t('form.name') }}
          <input id="name" class="form" :v-model="name" type="text" name="name"
        /></label>
        <label class="label">
          {{ $t('form.email') }}
          <input
            id="email"
            class="form"
            :v-model="namemaile"
            type="email"
            name="email"
        /></label>
        <div class="text-center pt-4">
          <button
            class="text-white border border-white px-5 py-2 rounded"
            @click="submit"
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
  data() {
    return {
      name: null,
      email: null,
    }
  },
  computed: {
    availableLocales() {
      return this.$i18n.locales.filter((i) => i.code !== this.$i18n.locale)
    },
  },
  methods: {
    submit() {
      this.$axios.$post(
        '/',
        {
          name: this.name,
        },
        {
          headers: {
            'Content-Type': 'multipart/form-data',
          },
        }
      )
    },
  },
}
</script>
