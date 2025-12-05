<template>
  <!-- Modal Overlay -->
  <transition
    enter-active-class="transition duration-300 ease-out"
    enter-from-class="opacity-0"
    enter-to-class="opacity-100"
    leave-active-class="transition duration-200 ease-in"
    leave-from-class="opacity-100"
    leave-to-class="opacity-0"
  >
    <div
      v-if="show"
      class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/60 backdrop-blur-sm"
      @click.self="closeModal"
    >
      <!-- Modal Content -->
      <transition
        enter-active-class="transition duration-300 ease-out"
        enter-from-class="opacity-0 scale-90 translate-y-4"
        enter-to-class="opacity-100 scale-100 translate-y-0"
        leave-active-class="transition duration-200 ease-in"
        leave-from-class="opacity-100 scale-100 translate-y-0"
        leave-to-class="opacity-0 scale-90 translate-y-4"
      >
        <div
          v-if="show"
          class="relative w-full max-w-lg bg-white rounded-3xl shadow-2xl overflow-hidden"
          @click.stop
        >
          <!-- Close Button -->
          <button
            @click="closeModal"
            class="absolute top-4 right-4 z-10 w-10 h-10 flex items-center justify-center rounded-full bg-white/90 hover:bg-white text-gray-600 hover:text-gray-900 transition-all duration-200 hover:scale-110 shadow-lg"
            aria-label="Close modal"
          >
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M6 18L18 6M6 6l12 12"/>
            </svg>
          </button>

          <!-- Gradient Background -->
          <div class="relative bg-gradient-to-br from-green-500 via-emerald-500 to-teal-500 px-8 py-12 text-center">
            <!-- Decorative circles -->
            <div class="absolute top-0 left-0 w-32 h-32 bg-white/10 rounded-full blur-2xl -translate-x-1/2 -translate-y-1/2"></div>
            <div class="absolute bottom-0 right-0 w-32 h-32 bg-white/10 rounded-full blur-2xl translate-x-1/2 translate-y-1/2"></div>
            
            <!-- Success Icon with Animation -->
            <div class="relative mb-6 inline-flex">
              <div class="absolute inset-0 bg-white/20 rounded-full animate-ping"></div>
              <div class="relative w-24 h-24 bg-white rounded-full flex items-center justify-center shadow-2xl">
                <svg class="w-14 h-14 text-green-500 animate-bounce" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="3" d="M5 13l4 4L19 7"/>
                </svg>
              </div>
            </div>

            <!-- Celebration Emojis -->
            <div class="absolute top-8 left-8 text-3xl animate-bounce" style="animation-delay: 0.1s">🎉</div>
            <div class="absolute top-12 right-12 text-3xl animate-bounce" style="animation-delay: 0.2s">✨</div>
            <div class="absolute bottom-16 left-12 text-3xl animate-bounce" style="animation-delay: 0.3s">💚</div>
            <div class="absolute bottom-12 right-8 text-3xl animate-bounce" style="animation-delay: 0.4s">🙏</div>

            <h2 class="text-4xl font-bold text-white mb-3 relative">
              Vielen Dank!
            </h2>
            <p class="text-xl text-white/95 relative">
              Ihre großzügige Spende macht einen echten Unterschied
            </p>
          </div>

          <!-- Content Section -->
          <div class="px-8 py-8 space-y-6">
            <!-- Donation Amount Display -->
            <div class="bg-gradient-to-br from-green-50 to-emerald-50 rounded-2xl p-6 border-2 border-green-200">
              <p class="text-sm font-medium text-gray-600 mb-1">Ihre Spende</p>
              <p class="text-4xl font-bold text-green-600">
                {{ formatCurrency(amount) }}
              </p>
            </div>

            <!-- Impact Message -->
            <div class="space-y-3">
              <div class="flex items-start gap-3">
                <div class="flex-shrink-0 w-8 h-8 bg-green-100 rounded-full flex items-center justify-center mt-0.5">
                  <svg class="w-5 h-5 text-green-600" fill="currentColor" viewBox="0 0 20 20">
                    <path fill-rule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z" clip-rule="evenodd"/>
                  </svg>
                </div>
                <div>
                  <p class="font-semibold text-gray-900">Hilfe kommt direkt an</p>
                  <p class="text-sm text-gray-600">100% Ihrer Spende geht direkt an bedürftige Familien</p>
                </div>
              </div>

              <div class="flex items-start gap-3">
                <div class="flex-shrink-0 w-8 h-8 bg-blue-100 rounded-full flex items-center justify-center mt-0.5">
                  <svg class="w-5 h-5 text-blue-600" fill="currentColor" viewBox="0 0 20 20">
                    <path d="M2.003 5.884L10 9.882l7.997-3.998A2 2 0 0016 4H4a2 2 0 00-1.997 1.884z"/>
                    <path d="M18 8.118l-8 4-8-4V14a2 2 0 002 2h12a2 2 0 002-2V8.118z"/>
                  </svg>
                </div>
                <div>
                  <p class="font-semibold text-gray-900">Spendenbescheinigung folgt</p>
                  <p class="text-sm text-gray-600">Sie erhalten eine E-Mail mit allen Details</p>
                </div>
              </div>

              <div class="flex items-start gap-3">
                <div class="flex-shrink-0 w-8 h-8 bg-purple-100 rounded-full flex items-center justify-center mt-0.5">
                  <svg class="w-5 h-5 text-purple-600" fill="currentColor" viewBox="0 0 20 20">
                    <path d="M9 6a3 3 0 11-6 0 3 3 0 016 0zM17 6a3 3 0 11-6 0 3 3 0 016 0zM12.93 17c.046-.327.07-.66.07-1a6.97 6.97 0 00-1.5-4.33A5 5 0 0119 16v1h-6.07zM6 11a5 5 0 015 5v1H1v-1a5 5 0 015-5z"/>
                  </svg>
                </div>
                <div>
                  <p class="font-semibold text-gray-900">Gemeinsam stark</p>
                  <p class="text-sm text-gray-600">Ihre Unterstützung inspiriert andere zu helfen</p>
                </div>
              </div>
            </div>

            <!-- Action Buttons -->
            <div class="flex gap-3 pt-4">
              <button
                @click="closeModal"
                class="flex-1 px-6 py-3 bg-gradient-to-r from-green-500 to-emerald-500 text-white font-bold rounded-xl hover:from-green-600 hover:to-emerald-600 transition-all duration-200 shadow-lg hover:shadow-xl hover:scale-105"
              >
                Schließen
              </button>
              <button
                @click="shareOnSocial"
                class="px-6 py-3 bg-gray-100 text-gray-700 font-semibold rounded-xl hover:bg-gray-200 transition-all duration-200 flex items-center gap-2"
              >
                <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 20 20">
                  <path d="M15 8a3 3 0 10-2.977-2.63l-4.94 2.47a3 3 0 100 4.319l4.94 2.47a3 3 0 10.895-1.789l-4.94-2.47a3.027 3.027 0 000-.74l4.94-2.47C13.456 7.68 14.19 8 15 8z"/>
                </svg>
                Teilen
              </button>
            </div>
          </div>
        </div>
      </transition>
    </div>
  </transition>
</template>

<script>
export default {
  name: 'ThankYouModal',
  props: {
    show: {
      type: Boolean,
      default: false
    },
    amount: {
      type: Number,
      default: 0
    }
  },
  emits: ['close'],
  methods: {
    closeModal() {
      this.$emit('close')
    },
    formatCurrency(amount) {
      return new Intl.NumberFormat('de-DE', {
        style: 'currency',
        currency: 'EUR',
        minimumFractionDigits: 0,
        maximumFractionDigits: 0
      }).format(amount)
    },
    shareOnSocial() {
      // Simple share functionality
      const text = `Ich habe gerade ${this.formatCurrency(this.amount)} gespendet, um Familien in Not zu helfen! 💚`
      if (navigator.share) {
        navigator.share({
          title: 'Meine Spende',
          text: text,
        }).catch(() => {})
      } else {
        // Fallback: Copy to clipboard
        navigator.clipboard.writeText(text)
        alert('Text in Zwischenablage kopiert!')
      }
    }
  }
}
</script>

<style scoped>
@keyframes bounce {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px);
  }
}

.animate-bounce {
  animation: bounce 1s infinite;
}
</style>
