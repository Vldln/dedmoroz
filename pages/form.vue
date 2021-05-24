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
      <div v-if="!success" class="flex justify-center text-gray-600">
        <nuxt-link
          v-for="locale in availableLocales"
          :key="locale.code"
          class="mr-3"
          :to="switchLocalePath(locale.code)"
          >{{ locale.name }}</nuxt-link
        >
      </div>
      <div
        v-if="success"
        class="text-3xl text-gray-200 sm:text-4xl pb-4 font-bold text-center"
      >
        {{ $t('form.sucess') }}
      </div>
      <div v-if="!success">
        <h1
          class="text-3xl text-gray-200 sm:text-4xl pb-4 font-bold text-center"
        >
          {{ $t('form.title') }}
        </h1>
        <form
          name="Apply"
          method="post"
          action="/success/"
          data-netlify="true"
          data-netlify-honeypot="bot-field"
          @submit.prevent="handleSubmit"
        >
          <input type="hidden" name="form-name" value="contact" />
          <p hidden>
            <label> Don’t fill this out: <input name="bot-field" /> </label>
          </p>
          <input type="hidden" name="form-name" value="ask-question" />
          <label class="label">
            {{ $t('form.name') }}
            <input
              id="name"
              v-model="formData.name"
              class="form"
              type="text"
              name="name"
          /></label>
          <label class="label">
            {{ $t('form.email') }}
            <input
              id="email"
              v-model="formData.email"
              class="form"
              type="email"
              name="email"
          /></label>
          <label class="label">
            {{ $t('form.country') }}
            <input
              id="country"
              v-model="formData.country"
              class="form"
              type="text"
              name="country"
          /></label>
          <label class="label">
            {{ $t('form.special') }}
            <input
              id="special"
              v-model="formData.special"
              class="form"
              type="text"
              name="special"
          /></label>
          <label class="label">
            {{ $t('form.arrive') }}
            <input
              id="arrive"
              v-model="formData.arrive"
              class="form"
              type="date"
              name="arrive"
          /></label>
          <label class="label">
            {{ $t('form.departure') }}
            <input
              id="departure"
              v-model="formData.departure"
              class="form"
              type="date"
              name="departure"
          /></label>
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
  </div>
</template>

<script>
export default {
  data() {
    return {
      formData: {},
      success: false,
    }
  },
  computed: {
    availableLocales() {
      return this.$i18n.locales.filter((i) => i.code !== this.$i18n.locale)
    },
  },
  methods: {
    encode(data) {
      return Object.keys(data)
        .map(
          (key) => encodeURIComponent(key) + '=' + encodeURIComponent(data[key])
        )
        .join('&')
    },
    handleSubmit(e) {
      fetch('/', {
        method: 'POST',
        headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
        body: this.encode({
          'form-name': e.target.getAttribute('name'),
          ...this.formData,
        }),
      })
        .then(() => (this.success = true))
        .catch((error) => alert(error))
    },
  },
}
</script>
