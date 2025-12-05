<template>
  <section class="py-16 md:py-20 lg:py-24 px-6 bg-gray-50">
    <div class="max-w-4xl mx-auto">
      <!-- Section Header -->
      <div class="text-center mb-12 md:mb-16">
        <h2 class="text-3xl md:text-4xl lg:text-5xl font-bold text-gray-900 mb-4">
          Häufig gestellte Fragen
        </h2>
        <p class="text-lg md:text-xl text-gray-600">
          Hier finden Sie Antworten auf die wichtigsten Fragen rund um Ihre Spende.
        </p>
      </div>

      <!-- FAQ Accordion List -->
      <div class="space-y-4 mb-12">
        <div
          v-for="faq in faqData"
          :key="faq.id"
          class="bg-white rounded-xl shadow-md overflow-hidden transition-all duration-300 border-2"
          :class="activeFaqId === faq.id ? 'shadow-xl border-primary-200' : 'border-transparent hover:shadow-lg'"
        >
          <button
            class="w-full px-6 py-5 md:px-8 md:py-6 text-left flex items-center justify-between gap-4 transition-colors duration-200"
            :class="activeFaqId === faq.id ? 'bg-primary-50/50' : 'hover:bg-gray-50'"
            @click="toggleFaq(faq.id)"
            :aria-expanded="activeFaqId === faq.id"
            :aria-controls="`faq-answer-${faq.id}`"
          >
            <span class="text-lg md:text-xl font-semibold text-gray-900 flex-1 leading-tight">
              {{ faq.question }}
            </span>
            <span 
              class="flex-shrink-0 text-primary-600 transition-transform duration-300"
              :class="{ 'rotate-180': activeFaqId === faq.id }"
            >
              <svg
                class="w-6 h-6"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2.5"
                  d="M19 9l-7 7-7-7"
                />
              </svg>
            </span>
          </button>
          
          <transition
            @enter="enter"
            @after-enter="afterEnter"
            @leave="leave"
          >
            <div
              v-show="activeFaqId === faq.id"
              :id="`faq-answer-${faq.id}`"
              class="overflow-hidden transition-all duration-300 ease-in-out"
            >
              <div class="px-6 pb-6 md:px-8 md:pb-8 text-gray-600 text-base md:text-lg leading-relaxed">
                {{ faq.answer }}
              </div>
            </div>
          </transition>
        </div>
      </div>

      <!-- Contact Card -->
      <div class="bg-gradient-to-br from-primary-600 to-blue-600 rounded-2xl shadow-2xl p-8 md:p-10 text-center text-white">
        <svg class="w-16 h-16 mx-auto mb-4 opacity-90" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"/>
        </svg>
        <p class="text-xl md:text-2xl font-semibold mb-6">
          Haben Sie weitere Fragen?
        </p>
        <button 
          @click="openContact"
          class="inline-flex items-center gap-2 px-6 py-3 bg-white text-primary-600 font-bold rounded-xl shadow-lg hover:shadow-xl transition-all duration-300 hover:scale-105 focus:outline-none focus:ring-4 focus:ring-white/30"
        >
          <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"/>
          </svg>
          Kontaktieren Sie uns
        </button>
      </div>
    </div>
  </section>
</template>

<script>
import { ref } from 'vue'
import faqData from '../data/faq.json'

export default {
  name: 'FaqSection',
  emits: ['open-contact'],
  setup(props, { emit }) {
    const activeFaqId = ref(null)

    const toggleFaq = (faqId) => {
      if (activeFaqId.value === faqId) {
        activeFaqId.value = null
      } else {
        activeFaqId.value = faqId
      }
    }

    // Accordion animation helpers
    const enter = (element) => {
      element.style.height = '0'
      element.style.opacity = '0'
    }

    const afterEnter = (element) => {
      element.style.height = 'auto'
      element.style.opacity = '1'
    }

    const leave = (element) => {
      element.style.height = `${element.scrollHeight}px`
      // Force reflow
      element.offsetHeight
      element.style.height = '0'
      element.style.opacity = '0'
    }

    const openContact = () => {
      emit('open-contact')
    }

    return {
      faqData,
      activeFaqId,
      toggleFaq,
      enter,
      afterEnter,
      leave,
      openContact
    }
  }
}
</script>

<style scoped>
/* All styling is now handled by Tailwind utility classes */
</style>
