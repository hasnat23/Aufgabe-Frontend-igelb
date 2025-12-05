<template>
  <section class="relative py-16 md:py-20 lg:py-24 px-6 bg-gradient-to-br from-rose-50 via-purple-50 to-indigo-100 overflow-hidden">
    <!-- Decorative Background Elements -->
    <div class="absolute inset-0 overflow-hidden pointer-events-none">
      <!-- Top Right Circle -->
      <div class="absolute -top-24 -right-24 w-96 h-96 bg-gradient-to-br from-purple-400/20 to-pink-400/20 rounded-full blur-3xl"></div>
      
      <!-- Bottom Left Circle -->
      <div class="absolute -bottom-32 -left-32 w-[500px] h-[500px] bg-gradient-to-tr from-blue-400/20 to-indigo-400/20 rounded-full blur-3xl"></div>
      
      <!-- Center Accent -->
      <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[600px] h-[600px] bg-gradient-to-br from-violet-300/10 to-fuchsia-300/10 rounded-full blur-3xl"></div>
      
      <!-- Floating Decorative Shapes -->
      <div class="absolute top-20 left-[10%] w-20 h-20 bg-gradient-to-br from-pink-300/30 to-rose-300/30 rounded-2xl rotate-12 blur-xl"></div>
      <div class="absolute top-40 right-[15%] w-32 h-32 bg-gradient-to-br from-purple-300/30 to-indigo-300/30 rounded-full blur-2xl"></div>
      <div class="absolute bottom-32 left-[20%] w-24 h-24 bg-gradient-to-br from-blue-300/30 to-cyan-300/30 rounded-3xl -rotate-12 blur-xl"></div>
      <div class="absolute bottom-48 right-[25%] w-16 h-16 bg-gradient-to-br from-violet-300/40 to-purple-300/40 rounded-full blur-lg"></div>
    </div>

    <div class="max-w-3xl mx-auto relative z-10">
      <!-- Section Header -->
      <div class="text-center mb-10 md:mb-12">
        <div class="inline-flex items-center justify-center w-16 h-16 mb-6 bg-gradient-to-br from-pink-500 to-violet-600 rounded-2xl shadow-xl">
          <svg class="w-8 h-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z"/>
          </svg>
        </div>
        <h2 class="text-3xl md:text-4xl lg:text-5xl font-bold bg-gradient-to-r from-purple-900 via-violet-900 to-indigo-900 bg-clip-text text-transparent mb-4">
          Jetzt spenden
        </h2>
        <p class="text-lg md:text-xl text-gray-700 font-medium">
          Jeder Beitrag zählt. Helfen Sie mit Ihrer Spende Menschen in Not.
        </p>
      </div>

      <!-- Donation Form -->
      <form @submit.prevent="handleSubmit" class="relative bg-white/90 backdrop-blur-xl border-2 border-white/60 rounded-3xl shadow-2xl p-6 md:p-8 lg:p-10 space-y-6" novalidate>
        <!-- Name Field -->
        <div>
          <label for="name" class="block text-sm font-bold text-gray-800 mb-2">
            Name <span class="text-rose-600">*</span>
          </label>
          <input
            id="name"
            v-model="formData.name"
            type="text"
            class="w-full px-4 py-3 border-2 rounded-xl text-base transition-all duration-200 focus:outline-none focus:ring-4 bg-white/80"
            :class="errors.name 
              ? 'border-red-500 focus:border-red-500 focus:ring-red-100' 
              : 'border-gray-200 focus:border-violet-500 focus:ring-violet-100'"
            placeholder="Ihr vollständiger Name"
            @input="clearError('name')"
          />
          <transition
            enter-active-class="transition duration-200 ease-out"
            enter-from-class="opacity-0 -translate-y-1"
            leave-active-class="transition duration-150 ease-in"
            leave-to-class="opacity-0 -translate-y-1"
          >
            <p v-if="errors.name" class="mt-2 text-sm font-medium text-red-600 flex items-center gap-1">
              <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 20 20">
                <path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7 4a1 1 0 11-2 0 1 1 0 012 0zm-1-9a1 1 0 00-1 1v4a1 1 0 102 0V6a1 1 0 00-1-1z" clip-rule="evenodd"/>
              </svg>
              {{ errors.name }}
            </p>
          </transition>
        </div>

        <!-- Email Field -->
        <div>
          <label for="email" class="block text-sm font-bold text-gray-800 mb-2">
            E-Mail <span class="text-rose-600">*</span>
          </label>
          <input
            id="email"
            v-model="formData.email"
            type="email"
            class="w-full px-4 py-3 border-2 rounded-xl text-base transition-all duration-200 focus:outline-none focus:ring-4 bg-white/80"
            :class="errors.email 
              ? 'border-red-500 focus:border-red-500 focus:ring-red-100' 
              : 'border-gray-200 focus:border-violet-500 focus:ring-violet-100'"
            placeholder="ihre.email@beispiel.de"
            @input="clearError('email')"
          />
          <transition
            enter-active-class="transition duration-200 ease-out"
            enter-from-class="opacity-0 -translate-y-1"
            leave-active-class="transition duration-150 ease-in"
            leave-to-class="opacity-0 -translate-y-1"
          >
            <p v-if="errors.email" class="mt-2 text-sm font-medium text-red-600 flex items-center gap-1">
              <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 20 20">
                <path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7 4a1 1 0 11-2 0 1 1 0 012 0zm-1-9a1 1 0 00-1 1v4a1 1 0 102 0V6a1 1 0 00-1-1z" clip-rule="evenodd"/>
              </svg>
              {{ errors.email }}
            </p>
          </transition>
        </div>

        <!-- Amount Field -->
        <div>
          <label for="amount" class="block text-sm font-bold text-gray-800 mb-2">
            Spendenbetrag <span class="text-rose-600">*</span>
          </label>
          <div class="relative">
            <span class="absolute left-4 top-1/2 -translate-y-1/2 text-violet-600 font-bold text-base pointer-events-none">
              €
            </span>
            <input
              id="amount"
              v-model.number="formData.amount"
              type="number"
              min="5"
              step="1"
              class="w-full pl-10 pr-4 py-3 border-2 rounded-xl text-base transition-all duration-200 focus:outline-none focus:ring-4 bg-white/80"
              :class="errors.amount 
                ? 'border-red-500 focus:border-red-500 focus:ring-red-100' 
                : 'border-gray-200 focus:border-violet-500 focus:ring-violet-100'"
              placeholder="Mindestens 5"
              @input="clearError('amount')"
            />
          </div>
          <transition
            enter-active-class="transition duration-200 ease-out"
            enter-from-class="opacity-0 -translate-y-1"
            leave-active-class="transition duration-150 ease-in"
            leave-to-class="opacity-0 -translate-y-1"
          >
            <p v-if="errors.amount" class="mt-2 text-sm font-medium text-red-600 flex items-center gap-1">
              <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 20 20">
                <path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7 4a1 1 0 11-2 0 1 1 0 012 0zm-1-9a1 1 0 00-1 1v4a1 1 0 102 0V6a1 1 0 00-1-1z" clip-rule="evenodd"/>
              </svg>
              {{ errors.amount }}
            </p>
          </transition>
          
          <!-- Quick Amount Buttons -->
          <div class="mt-4 flex flex-wrap gap-2">
            <button
              v-for="quickAmount in quickAmounts"
              :key="quickAmount"
              type="button"
              class="px-4 py-2 border-2 rounded-lg text-sm font-bold transition-all duration-200 hover:scale-105"
              :class="formData.amount === quickAmount 
                ? 'bg-gradient-to-r from-violet-600 to-purple-600 border-transparent text-white shadow-lg shadow-violet-300/50' 
                : 'bg-white/80 border-gray-200 text-gray-700 hover:border-violet-400 hover:text-violet-700 hover:bg-violet-50'"
              @click="selectQuickAmount(quickAmount)"
            >
              {{ quickAmount }} €
            </button>
          </div>
        </div>

        <!-- Newsletter Checkbox -->
        <div class="pt-2">
          <label class="flex items-start gap-3 cursor-pointer group">
            <input
              v-model="formData.newsletter"
              type="checkbox"
              class="w-5 h-5 mt-0.5 rounded border-2 border-gray-300 text-violet-600 focus:ring-4 focus:ring-violet-100 transition-all duration-200 cursor-pointer"
            />
            <span class="text-sm text-gray-700 leading-relaxed group-hover:text-gray-900 transition-colors font-medium">
              Ich möchte den Newsletter erhalten und über zukünftige Projekte informiert werden.
            </span>
          </label>
        </div>

        <!-- Submit Button -->
        <button
          type="submit"
          class="relative w-full mt-8 px-6 py-4 bg-gradient-to-r from-pink-600 via-purple-600 to-violet-600 text-white text-lg font-bold rounded-xl shadow-xl shadow-purple-300/50 transition-all duration-300 hover:shadow-2xl hover:shadow-purple-400/60 hover:-translate-y-1 hover:scale-[1.02] focus:outline-none focus:ring-4 focus:ring-purple-300 disabled:opacity-60 disabled:cursor-not-allowed disabled:hover:translate-y-0 disabled:hover:shadow-xl overflow-hidden"
          :disabled="isSubmitting"
        >
          <div class="absolute inset-0 bg-gradient-to-r from-pink-500 via-purple-500 to-violet-500 opacity-0 hover:opacity-100 transition-opacity duration-300"></div>
          <span v-if="!isSubmitting" class="relative flex items-center justify-center gap-2">
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z"/>
            </svg>
            Jetzt spenden
          </span>
          <span v-else class="relative flex items-center justify-center gap-2">
            <svg class="animate-spin h-5 w-5" fill="none" viewBox="0 0 24 24">
              <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
              <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
            </svg>
            Wird verarbeitet...
          </span>
        </button>

        <p class="text-center text-sm text-gray-600 mt-4 font-medium">
          <span class="text-rose-600">*</span> Pflichtfelder
        </p>
      </form>
    </div>
  </section>
</template>

<script>
import { reactive, ref } from 'vue'

export default {
  name: 'DonationForm',
  emits: ['donation-submitted'],
  setup(props, { emit }) {
    const formData = reactive({
      name: '',
      email: '',
      amount: null,
      newsletter: false
    })

    const errors = reactive({
      name: '',
      email: '',
      amount: ''
    })

    const isSubmitting = ref(false)
    const quickAmounts = [5, 10, 25, 50, 100]

    const validateForm = () => {
      let isValid = true

      // Reset errors
      errors.name = ''
      errors.email = ''
      errors.amount = ''

      // Validate name
      if (!formData.name.trim()) {
        errors.name = 'Bitte geben Sie Ihren Namen ein.'
        isValid = false
      } else if (formData.name.trim().length < 2) {
        errors.name = 'Der Name muss mindestens 2 Zeichen lang sein.'
        isValid = false
      }

      // Validate email
      if (!formData.email.trim()) {
        errors.email = 'Bitte geben Sie Ihre E-Mail-Adresse ein.'
        isValid = false
      } else {
        const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
        if (!emailRegex.test(formData.email)) {
          errors.email = 'Bitte geben Sie eine gültige E-Mail-Adresse ein.'
          isValid = false
        }
      }

      // Validate amount
      if (!formData.amount) {
        errors.amount = 'Bitte geben Sie einen Spendenbetrag ein.'
        isValid = false
      } else if (formData.amount < 5) {
        errors.amount = 'Der Mindestbetrag beträgt 5 €.'
        isValid = false
      } else if (formData.amount > 1000000) {
        errors.amount = 'Der Betrag ist zu hoch. Bitte kontaktieren Sie uns direkt.'
        isValid = false
      }

      return isValid
    }

    const clearError = (field) => {
      errors[field] = ''
    }

    const selectQuickAmount = (amount) => {
      formData.amount = amount
      clearError('amount')
    }

    const handleSubmit = async () => {
      if (!validateForm()) {
        // Find first error field and focus it
        const firstErrorField = Object.keys(errors).find(key => errors[key])
        if (firstErrorField) {
          const element = document.getElementById(firstErrorField)
          if (element) {
            element.focus()
            element.scrollIntoView({ behavior: 'smooth', block: 'center' })
          }
        }
        return
      }

      isSubmitting.value = true

      // Simulate API call
      await new Promise(resolve => setTimeout(resolve, 800))

      // Emit donation event
      emit('donation-submitted', formData.amount)

      // Reset form
      formData.name = ''
      formData.email = ''
      formData.amount = null
      formData.newsletter = false

      isSubmitting.value = false
    }

    return {
      formData,
      errors,
      isSubmitting,
      quickAmounts,
      handleSubmit,
      clearError,
      selectQuickAmount
    }
  }
}
</script>

<style scoped>
/* Remove number input arrows - Tailwind doesn't handle these */
input[type=number]::-webkit-inner-spin-button,
input[type=number]::-webkit-outer-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

input[type=number] {
  -moz-appearance: textfield;
  appearance: textfield;
}
</style>
