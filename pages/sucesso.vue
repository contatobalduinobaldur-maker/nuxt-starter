<template>
  <main class="min-h-screen flex items-center justify-center px-6 py-16">
    <section class="w-full max-w-xl rounded-2xl shadow-lg p-8">
      <header class="mb-6 text-center">
        <h1 class="text-3xl font-bold">Obrigado! 🎉</h1>
        <p class="mt-2 text-gray-600">
          Recebemos os teus dados e já estamos a preparar o contacto.
        </p>
      </header>

      <div class="space-y-4">
        <div class="rounded-xl p-4 bg-gray-50">
          <p class="text-sm text-gray-700">
            <strong>Próximo passo:</strong> fala connosco agora mesmo no WhatsApp
            e acelera o teu atendimento.
          </p>
        </div>

        <a
          :href="whatsAppUrl"
          class="block w-full text-center rounded-xl px-5 py-3 font-semibold shadow hover:opacity-95 transition"
          style="background:#25D366;color:white"
        >
          Falar no WhatsApp
        </a>

        <NuxtLink
          to="/"
          class="block w-full text-center rounded-xl px-5 py-3 font-medium border"
        >
          Voltar à página inicial
        </NuxtLink>

        <details class="mt-2">
          <summary class="cursor-pointer text-sm text-gray-600">O que acontece a seguir?</summary>
          <ul class="mt-2 text-sm text-gray-600 list-disc pl-5 space-y-1">
            <li>Registámos o teu pedido e em breve receberás resposta.</li>
            <li>Se nos chamares no WhatsApp, conseguimos priorizar o teu atendimento.</li>
            <li>Guarda este link para consultar as novidades e oportunidades.</li>
          </ul>
        </details>
      </div>

      <footer class="mt-8 text-center text-xs text-gray-500">
        Ref.: <code>{{ refResumo }}</code>
      </footer>
    </section>
  </main>
</template>

<script setup>
const numeroWhatsApp = '5511969445832' // teu número (DDI+DDD+núm) sem espaços

const route = useRoute()
const origem = route.query.utm_source || route.query.source || 'landing'
const campanha = route.query.utm_campaign || 'default'
const msg = `Olá! Acabei de enviar o formulário na landing. Origem: ${origem} | Campanha: ${campanha}. Podemos falar agora?`

const whatsAppUrl = computed(() =>
  `https://wa.me/${numeroWhatsApp}?text=${encodeURIComponent(msg)}`
)

onMounted(() => {
  // GA4 (dataLayer/gtag) e Meta Pixel, se existirem
  if (typeof window !== 'undefined') {
    window.dataLayer = window.dataLayer || []
    window.dataLayer.push({
      event: 'lead_submitted',
      source: origem,
      campaign: campanha,
    })
    if (typeof window.gtag === 'function') {
      window.gtag('event', 'generate_lead', { source: origem, campaign: campanha })
    }
    if (typeof window.fbq === 'function') {
      window.fbq('track', 'Lead', { source: origem, campaign: campanha })
    }
  }

  // 👉 Se quiseres abrir o WhatsApp automaticamente ao chegar aqui, descomenta:
  // setTimeout(() => { window.location.href = whatsAppUrl.value }, 800)
})

const refResumo = computed(() => {
  const qs = new URLSearchParams(route.query).toString()
  return qs ? `?${qs}` : '—'
})
</script>

<style scoped>
main { background: #f7f7f9; }
section { background: white; }
</style>

