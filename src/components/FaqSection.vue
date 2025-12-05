<template>
  <section class="relative py-16 md:py-20 lg:py-24 px-6 bg-gradient-to-br from-indigo-50 via-blue-50 to-cyan-100 overflow-hidden">
    <!-- Decorative Background Elements -->
    <div class="absolute inset-0 overflow-hidden pointer-events-none">
      <!-- Top Left Circle -->
      <div class="absolute -top-32 -left-32 w-[500px] h-[500px] bg-gradient-to-br from-blue-400/20 to-indigo-400/20 rounded-full blur-3xl"></div>
      
      <!-- Bottom Right Circle -->
      <div class="absolute -bottom-24 -right-24 w-96 h-96 bg-gradient-to-tr from-cyan-400/20 to-blue-400/20 rounded-full blur-3xl"></div>
      
      <!-- Center Accent -->
      <div class="absolute top-1/3 left-1/2 -translate-x-1/2 w-[600px] h-[600px] bg-gradient-to-br from-indigo-300/10 to-blue-300/10 rounded-full blur-3xl"></div>
      
      <!-- Floating Decorative Shapes -->
      <div class="absolute top-32 right-[15%] w-24 h-24 bg-gradient-to-br from-cyan-300/30 to-blue-300/30 rounded-2xl rotate-12 blur-xl"></div>
      <div class="absolute top-48 left-[10%] w-32 h-32 bg-gradient-to-br from-indigo-300/30 to-violet-300/30 rounded-full blur-2xl"></div>
      <div class="absolute bottom-40 right-[20%] w-20 h-20 bg-gradient-to-br from-blue-300/40 to-cyan-300/40 rounded-3xl -rotate-12 blur-xl"></div>
    </div>

    <div class="max-w-4xl mx-auto relative z-10">
      <!-- Section Header -->
      <div class="text-center mb-12 md:mb-16">
        <div class="inline-flex items-center justify-center w-16 h-16 mb-6 bg-gradient-to-br from-blue-500 to-indigo-600 rounded-2xl shadow-xl">
          <svg class="w-8 h-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8.228 9c.549-1.165 2.03-2 3.772-2 2.21 0 4 1.343 4 3 0 1.4-1.278 2.575-3.006 2.907-.542.104-.994.54-.994 1.093m0 3h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"/>
          </svg>
        </div>
        <h2 class="text-3xl md:text-4xl lg:text-5xl font-bold bg-gradient-to-r from-blue-900 via-indigo-900 to-violet-900 bg-clip-text text-transparent mb-4">
          Häufig gestellte Fragen
        </h2>
        <p class="text-lg md:text-xl text-gray-700 font-medium">
          Hier finden Sie Antworten auf die wichtigsten Fragen rund um Ihre Spende.
        </p>
      </div>

      <!-- FAQ Accordion List -->
      <div class="space-y-4 mb-12">
        <div
          v-for="faq in faqData"
          :key="faq.id"
          class="bg-white/90 backdrop-blur-xl rounded-2xl shadow-lg overflow-hidden transition-all duration-300 border-2"
          :class="activeFaqId === faq.id ? 'shadow-2xl shadow-blue-200/50 border-blue-300/60 scale-[1.02]' : 'border-white/60 hover:shadow-xl hover:border-blue-200/50'"
        >
          <button
            class="w-full px-6 py-5 md:px-8 md:py-6 text-left flex items-center justify-between gap-4 transition-colors duration-200"
            :class="activeFaqId === faq.id ? 'bg-gradient-to-r from-blue-50/80 to-indigo-50/80' : 'hover:bg-blue-50/50'"
            @click="toggleFaq(faq.id)"
            :aria-expanded="activeFaqId === faq.id"
            :aria-controls="`faq-answer-${faq.id}`"
          >
            <span class="text-lg md:text-xl font-bold text-gray-900 flex-1 leading-tight">
              {{ faq.question }}
            </span>
            <span 
              class="flex-shrink-0 transition-all duration-300"
              :class="activeFaqId === faq.id ? 'rotate-180 text-blue-600' : 'text-indigo-600'"
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
              <div class="px-6 pb-6 md:px-8 md:pb-8 text-gray-700 text-base md:text-lg leading-relaxed font-medium bg-gradient-to-b from-blue-50/30 to-transparent">
                {{ faq.answer }}
              </div>
            </div>
          </transition>
        </div>
      </div>

      <!-- Contact Card -->
      <div class="relative bg-gradient-to-br from-blue-600 via-indigo-600 to-violet-700 rounded-3xl shadow-2xl shadow-blue-300/50 p-8 md:p-10 text-center text-white overflow-hidden">
        <!-- Decorative elements -->
        <div class="absolute top-0 right-0 w-64 h-64 bg-white/10 rounded-full blur-3xl -translate-y-1/2 translate-x-1/2"></div>
        <div class="absolute bottom-0 left-0 w-48 h-48 bg-indigo-400/20 rounded-full blur-2xl translate-y-1/2 -translate-x-1/2"></div>
        
        <div class="relative z-10">
          <div class="inline-flex items-center justify-center w-16 h-16 mx-auto mb-4 bg-white/20 backdrop-blur-sm rounded-2xl">
            <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"/>
            </svg>
          </div>
          <p class="text-xl md:text-2xl font-bold mb-2">
            Haben Sie weitere Fragen?
          </p>
          <p class="text-blue-100 mb-6 text-base md:text-lg">
            Wir helfen Ihnen gerne weiter!
          </p>
          <button 
            @click="openContact"
            class="inline-flex items-center gap-2 px-6 py-3 bg-white text-indigo-700 font-bold rounded-xl shadow-lg hover:shadow-2xl transition-all duration-300 hover:scale-105 hover:-translate-y-1 focus:outline-none focus:ring-4 focus:ring-white/30"
          >
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"/>
            </svg>
            Kontakt aufnehmen
          </button>
        </div>
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
