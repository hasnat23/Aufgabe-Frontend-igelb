<template>
  <section class="py-16 md:py-20 lg:py-24 px-6 bg-white">
    <div class="max-w-3xl mx-auto">
      <!-- Section Header -->
      <div class="text-center mb-10 md:mb-12">
        <h2 class="text-3xl md:text-4xl lg:text-5xl font-bold text-gray-900 mb-4">
          Jetzt spenden
        </h2>
        <p class="text-lg md:text-xl text-gray-600">
          Jeder Beitrag zählt. Helfen Sie mit Ihrer Spende Menschen in Not.
        </p>
      </div>

      <!-- Donation Form -->
      <form @submit.prevent="handleSubmit" class="bg-white border-2 border-gray-200 rounded-2xl shadow-xl p-6 md:p-8 lg:p-10 space-y-6" novalidate>
        <!-- Name Field -->
        <div>
          <label for="name" class="block text-sm font-semibold text-gray-700 mb-2">
            Name <span class="text-red-600">*</span>
          </label>
          <input
            id="name"
            v-model="formData.name"
            type="text"
            class="w-full px-4 py-3 border-2 rounded-xl text-base transition-all duration-200 focus:outline-none focus:ring-4"
            :class="errors.name 
              ? 'border-red-500 focus:border-red-500 focus:ring-red-100' 
              : 'border-gray-300 focus:border-primary-600 focus:ring-primary-100'"
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
          <label for="email" class="block text-sm font-semibold text-gray-700 mb-2">
            E-Mail <span class="text-red-600">*</span>
          </label>
          <input
            id="email"
            v-model="formData.email"
            type="email"
            class="w-full px-4 py-3 border-2 rounded-xl text-base transition-all duration-200 focus:outline-none focus:ring-4"
            :class="errors.email 
              ? 'border-red-500 focus:border-red-500 focus:ring-red-100' 
              : 'border-gray-300 focus:border-primary-600 focus:ring-primary-100'"
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
          <label for="amount" class="block text-sm font-semibold text-gray-700 mb-2">
            Spendenbetrag <span class="text-red-600">*</span>
          </label>
          <div class="relative">
            <span class="absolute left-4 top-1/2 -translate-y-1/2 text-gray-600 font-semibold text-base pointer-events-none">
              €
            </span>
            <input
              id="amount"
              v-model.number="formData.amount"
              type="number"
              min="5"
              step="1"
              class="w-full pl-10 pr-4 py-3 border-2 rounded-xl text-base transition-all duration-200 focus:outline-none focus:ring-4"
              :class="errors.amount 
                ? 'border-red-500 focus:border-red-500 focus:ring-red-100' 
                : 'border-gray-300 focus:border-primary-600 focus:ring-primary-100'"
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
              class="px-4 py-2 border-2 rounded-lg text-sm font-semibold transition-all duration-200 hover:scale-105"
              :class="formData.amount === quickAmount 
                ? 'bg-primary-600 border-primary-600 text-white shadow-lg' 
                : 'bg-white border-gray-300 text-gray-700 hover:border-primary-600 hover:text-primary-600 hover:bg-primary-50'"
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
              class="w-5 h-5 mt-0.5 rounded border-2 border-gray-300 text-primary-600 focus:ring-4 focus:ring-primary-100 transition-all duration-200 cursor-pointer"
            />
            <span class="text-sm text-gray-600 leading-relaxed group-hover:text-gray-900 transition-colors">
              Ich möchte den Newsletter erhalten und über zukünftige Projekte informiert werden.
            </span>
          </label>
        </div>

        <!-- Submit Button -->
        <button
          type="submit"
          class="w-full mt-8 px-6 py-4 bg-gradient-to-r from-primary-600 to-blue-600 text-white text-lg font-bold rounded-xl shadow-lg transition-all duration-300 hover:shadow-2xl hover:-translate-y-1 focus:outline-none focus:ring-4 focus:ring-primary-200 disabled:opacity-60 disabled:cursor-not-allowed disabled:hover:translate-y-0 disabled:hover:shadow-lg"
          :disabled="isSubmitting"
        >
          <span v-if="!isSubmitting" class="flex items-center justify-center gap-2">
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z"/>
            </svg>
            Jetzt spenden
          </span>
          <span v-else class="flex items-center justify-center gap-2">
            <svg class="animate-spin h-5 w-5" fill="none" viewBox="0 0 24 24">
              <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
              <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
            </svg>
            Wird verarbeitet...
          </span>
        </button>

        <p class="text-center text-sm text-gray-500 mt-4">
          <span class="text-red-600">*</span> Pflichtfelder
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
