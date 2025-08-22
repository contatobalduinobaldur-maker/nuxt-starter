<script setup>
Paiges/index.vue '@/data/index.json'
const page = ref(pageData)

definePageMeta({
  layout: "default",
});
</script>

<template>
  <Container>
    <Hero
      :title="page.hero.title"
      :description="page.hero.description"
      :image="page.hero.image"
      :imageAlt="page.hero.imageAlt"
      :buttons="page.hero.buttons"
    ></Hero>
    <Logos :title="page.logos.title" :icons="page.logos.icons"></Logos>
    <Features
      :title="page.features.title"
      :description="page.features.description"
      :items="page.features.items"
    ></Features>
    <Testimonials
      :title="page.testimonials.title"
      :description="page.testimonials.description"
      :items="page.testimonials.items"
    ></Testimonials>
    <Cta
      :title="page.cta.title"
      :description="page.cta.description"
      :buttons="page.cta.buttons"
    ></Cta><!-- Lead Form -->
<section id="contact" class="py-16">
  <div class="max-w-2xl mx-auto">
    <h2 class="text-2xl font-bold mb-4">Pede mais informações</h2>

    <form
      name="lead-form"
      method="POST"
      data-netlify="true"
      netlify-honeypot="bot-field"
      action="/sucesso"
      class="space-y-4"
    >
      <input type="hidden" name="form-name" value="lead-form" />
      <p hidden>
        <label>Não preencher: <input name="bot-field" /></label>
      </p>

      <div>
        <label class="block text-sm font-medium">Nome</label>
        <input class="w-full border rounded p-3" type="text" name="nome" required />
      </div>

      <div>
        <label class="block text-sm font-medium">Email</label>
        <input class="w-full border rounded p-3" type="email" name="email" required />
      </div>

      <div>
        <label class="block text-sm font-medium">WhatsApp</label>
        <input class="w-full border rounded p-3" type="tel" name="whatsapp" required />
      </div>

      <button type="submit" class="w-full rounded-lg p-3 font-semibold border">
        Enviar
      </button>
    </form>
  </div>
</section>

  </Container>
</template>
