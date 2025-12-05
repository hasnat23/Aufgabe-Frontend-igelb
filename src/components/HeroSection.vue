<template>
  <section class="relative overflow-hidden bg-gradient-to-br from-indigo-600 via-purple-600 to-purple-700 text-white py-16 md:py-20 lg:py-24 px-6">
    <!-- Decorative background elements -->
    <div class="absolute inset-0 overflow-hidden pointer-events-none">
      <div class="absolute top-0 left-0 w-96 h-96 bg-white/10 rounded-full blur-3xl -translate-x-1/2 -translate-y-1/2"></div>
      <div class="absolute bottom-0 right-0 w-96 h-96 bg-white/10 rounded-full blur-3xl translate-x-1/2 translate-y-1/2"></div>
    </div>

    <div class="max-w-4xl mx-auto relative z-10">
      <!-- Hero Content -->
      <div class="text-center mb-12 md:mb-16 animate-slide-up">
        <h1 class="text-4xl md:text-5xl lg:text-6xl font-bold mb-4 md:mb-6 leading-tight">
          Gemeinsam Hoffnung schenken
        </h1>
        <p class="text-lg md:text-xl text-white/95 max-w-2xl mx-auto leading-relaxed">
          Ihre Spende macht einen Unterschied. Helfen Sie uns, Familien in Not zu unterstützen 
          und eine bessere Zukunft für alle zu schaffen.
        </p>
      </div>

      <!-- Donation Barometer Card -->
      <div class="bg-white/95 backdrop-blur-xl rounded-2xl shadow-2xl p-6 md:p-8 lg:p-10 text-gray-900 animate-fade-in">
        <div class="mb-6 md:mb-8">
          <h2 class="text-2xl md:text-3xl font-bold mb-3 text-gray-900">
            Spendenbarometer
          </h2>
          <div class="flex items-baseline gap-2 flex-wrap">
            <span class="text-3xl md:text-4xl lg:text-5xl font-bold text-primary-600">
              {{ formatCurrency(currentAmount) }}
            </span>
            <span class="text-xl md:text-2xl text-gray-500">
              von {{ formatCurrency(goalAmount) }}
            </span>
          </div>
        </div>
        
        <!-- Progress Bar -->
        <div class="relative h-10 md:h-12 bg-gray-200 rounded-full overflow-hidden mb-6 md:mb-8 shadow-inner">
          <div 
            class="absolute inset-y-0 left-0 rounded-full transition-all duration-700 ease-out flex items-center justify-end px-4"
            :class="isGoalReached ? 'bg-gradient-to-r from-green-500 to-green-600' : 'bg-gradient-to-r from-primary-600 to-blue-500'"
            :style="{ width: progressPercentage + '%' }"
          >
            <!-- Shimmer effect -->
            <div class="absolute inset-0 overflow-hidden">
              <div class="absolute inset-0 bg-gradient-to-r from-transparent via-white/30 to-transparent animate-shimmer"></div>
            </div>
            
            <span v-if="progressPercentage > 10" class="relative z-10 text-white font-bold text-sm md:text-base">
              {{ progressPercentage }}%
            </span>
          </div>
        </div>
        
        <!-- Stats Grid -->
        <div class="grid grid-cols-2 gap-4 md:gap-6">
          <div class="bg-gradient-to-br from-primary-50 to-blue-50 rounded-xl p-4 md:p-6 text-center border border-primary-100">
            <div class="text-2xl md:text-3xl lg:text-4xl font-bold text-primary-600 mb-1">
              {{ progressPercentage }}%
            </div>
            <div class="text-sm md:text-base text-gray-600 font-medium">
              Erreicht
            </div>
          </div>
          <div class="bg-gradient-to-br from-gray-50 to-gray-100 rounded-xl p-4 md:p-6 text-center border border-gray-200">
            <div class="text-2xl md:text-3xl lg:text-4xl font-bold text-gray-700 mb-1">
              {{ formatCurrency(remainingAmount) }}
            </div>
            <div class="text-sm md:text-base text-gray-600 font-medium">
              Noch benötigt
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import { computed } from 'vue'

export default {
  name: 'HeroSection',
  props: {
    currentAmount: {
      type: Number,
      required: true
    },
    goalAmount: {
      type: Number,
      required: true
    }
  },
  setup(props) {
    const progressPercentage = computed(() => {
      const percentage = (props.currentAmount / props.goalAmount) * 100
      return Math.min(Math.round(percentage), 100)
    })

    const remainingAmount = computed(() => {
      return Math.max(props.goalAmount - props.currentAmount, 0)
    })

    const isGoalReached = computed(() => {
      return props.currentAmount >= props.goalAmount
    })

    const formatCurrency = (amount) => {
      return new Intl.NumberFormat('de-DE', {
        style: 'currency',
        currency: 'EUR',
        minimumFractionDigits: 0,
        maximumFractionDigits: 0
      }).format(amount)
    }

    return {
      progressPercentage,
      remainingAmount,
      isGoalReached,
      formatCurrency
    }
  }
}
</script>

<style scoped>
/* All styling is now handled by Tailwind utility classes */
</style>
