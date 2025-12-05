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
          class="relative w-full max-w-2xl bg-white rounded-3xl shadow-2xl overflow-hidden max-h-[90vh] flex flex-col"
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

          <!-- Header -->
          <div class="bg-gradient-to-br from-primary-600 via-blue-600 to-indigo-600 px-8 py-10 text-center relative overflow-hidden">
            <!-- Decorative elements -->
            <div class="absolute top-0 left-0 w-40 h-40 bg-white/10 rounded-full blur-3xl -translate-x-1/2 -translate-y-1/2"></div>
            <div class="absolute bottom-0 right-0 w-40 h-40 bg-white/10 rounded-full blur-3xl translate-x-1/2 translate-y-1/2"></div>
            
            <div class="relative">
              <div class="inline-flex items-center justify-center w-16 h-16 bg-white/20 rounded-2xl mb-4 backdrop-blur-sm">
                <svg class="w-8 h-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"/>
                </svg>
              </div>
              <h2 class="text-3xl md:text-4xl font-bold text-white mb-2">
                Kontaktieren Sie uns
              </h2>
              <p class="text-lg text-white/90">
                Wir freuen uns auf Ihre Nachricht
              </p>
            </div>
          </div>

          <!-- Success Message -->
          <transition
            enter-active-class="transition duration-300 ease-out"
            enter-from-class="opacity-0 -translate-y-2"
            leave-active-class="transition duration-200 ease-in"
            leave-to-class="opacity-0 -translate-y-2"
          >
            <div v-if="showSuccess" class="mx-8 mt-6 bg-green-50 border-2 border-green-200 rounded-xl p-4 flex items-start gap-3">
              <svg class="w-6 h-6 text-green-600 flex-shrink-0 mt-0.5" fill="currentColor" viewBox="0 0 20 20">
                <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"/>
              </svg>
              <div>
                <p class="font-semibold text-green-900">Nachricht erfolgreich gesendet!</p>
                <p class="text-sm text-green-700">Wir melden uns schnellstmöglich bei Ihnen.</p>
              </div>
            </div>
          </transition>

          <!-- Form Content - Scrollable -->
          <div class="flex-1 overflow-y-auto px-8 py-8">
            <form @submit.prevent="handleSubmit" class="space-y-6" novalidate>
              <!-- Name Field -->
              <div>
                <label for="contact-name" class="block text-sm font-semibold text-gray-700 mb-2">
                  Name <span class="text-red-600">*</span>
                </label>
                <input
                  id="contact-name"
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
                <label for="contact-email" class="block text-sm font-semibold text-gray-700 mb-2">
                  E-Mail <span class="text-red-600">*</span>
                </label>
                <input
                  id="contact-email"
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

              <!-- Subject Field -->
              <div>
                <label for="contact-subject" class="block text-sm font-semibold text-gray-700 mb-2">
                  Betreff <span class="text-red-600">*</span>
                </label>
                <input
                  id="contact-subject"
                  v-model="formData.subject"
                  type="text"
                  class="w-full px-4 py-3 border-2 rounded-xl text-base transition-all duration-200 focus:outline-none focus:ring-4"
                  :class="errors.subject 
                    ? 'border-red-500 focus:border-red-500 focus:ring-red-100' 
                    : 'border-gray-300 focus:border-primary-600 focus:ring-primary-100'"
                  placeholder="Worum geht es?"
                  @input="clearError('subject')"
                />
                <transition
                  enter-active-class="transition duration-200 ease-out"
                  enter-from-class="opacity-0 -translate-y-1"
                  leave-active-class="transition duration-150 ease-in"
                  leave-to-class="opacity-0 -translate-y-1"
                >
                  <p v-if="errors.subject" class="mt-2 text-sm font-medium text-red-600 flex items-center gap-1">
                    <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 20 20">
                      <path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7 4a1 1 0 11-2 0 1 1 0 012 0zm-1-9a1 1 0 00-1 1v4a1 1 0 102 0V6a1 1 0 00-1-1z" clip-rule="evenodd"/>
                    </svg>
                    {{ errors.subject }}
                  </p>
                </transition>
              </div>

              <!-- Message Field -->
              <div>
                <label for="contact-message" class="block text-sm font-semibold text-gray-700 mb-2">
                  Nachricht <span class="text-red-600">*</span>
                </label>
                <textarea
                  id="contact-message"
                  v-model="formData.message"
                  rows="5"
                  class="w-full px-4 py-3 border-2 rounded-xl text-base transition-all duration-200 focus:outline-none focus:ring-4 resize-none"
                  :class="errors.message 
                    ? 'border-red-500 focus:border-red-500 focus:ring-red-100' 
                    : 'border-gray-300 focus:border-primary-600 focus:ring-primary-100'"
                  placeholder="Ihre Nachricht an uns..."
                  @input="clearError('message')"
                ></textarea>
                <transition
                  enter-active-class="transition duration-200 ease-out"
                  enter-from-class="opacity-0 -translate-y-1"
                  leave-active-class="transition duration-150 ease-in"
                  leave-to-class="opacity-0 -translate-y-1"
                >
                  <p v-if="errors.message" class="mt-2 text-sm font-medium text-red-600 flex items-center gap-1">
                    <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 20 20">
                      <path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7 4a1 1 0 11-2 0 1 1 0 012 0zm-1-9a1 1 0 00-1 1v4a1 1 0 102 0V6a1 1 0 00-1-1z" clip-rule="evenodd"/>
                    </svg>
                    {{ errors.message }}
                  </p>
                </transition>
              </div>

              <!-- Submit Button -->
              <button
                type="submit"
                class="w-full px-6 py-4 bg-gradient-to-r from-primary-600 to-blue-600 text-white text-lg font-bold rounded-xl shadow-lg transition-all duration-300 hover:shadow-2xl hover:-translate-y-1 focus:outline-none focus:ring-4 focus:ring-primary-200 disabled:opacity-60 disabled:cursor-not-allowed disabled:hover:translate-y-0 disabled:hover:shadow-lg flex items-center justify-center gap-2"
                :disabled="isSubmitting"
              >
                <span v-if="!isSubmitting">
                  <svg class="w-5 h-5 inline-block mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 19l9 2-9-18-9 18 9-2zm0 0v-8"/>
                  </svg>
                  Nachricht senden
                </span>
                <span v-else class="flex items-center gap-2">
                  <svg class="animate-spin h-5 w-5" fill="none" viewBox="0 0 24 24">
                    <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                    <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
                  </svg>
                  Wird gesendet...
                </span>
              </button>

              <p class="text-center text-sm text-gray-500">
                <span class="text-red-600">*</span> Pflichtfelder
              </p>
            </form>
          </div>
        </div>
      </transition>
    </div>
  </transition>
</template>

<script>
import { reactive, ref } from 'vue'

export default {
  name: 'ContactModal',
  props: {
    show: {
      type: Boolean,
      default: false
    }
  },
  emits: ['close'],
  setup(props, { emit }) {
    const formData = reactive({
      name: '',
      email: '',
      subject: '',
      message: ''
    })

    const errors = reactive({
      name: '',
      email: '',
      subject: '',
      message: ''
    })

    const isSubmitting = ref(false)
    const showSuccess = ref(false)

    const validateForm = () => {
      let isValid = true

      // Reset errors
      errors.name = ''
      errors.email = ''
      errors.subject = ''
      errors.message = ''

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

      // Validate subject
      if (!formData.subject.trim()) {
        errors.subject = 'Bitte geben Sie einen Betreff ein.'
        isValid = false
      } else if (formData.subject.trim().length < 3) {
        errors.subject = 'Der Betreff muss mindestens 3 Zeichen lang sein.'
        isValid = false
      }

      // Validate message
      if (!formData.message.trim()) {
        errors.message = 'Bitte geben Sie eine Nachricht ein.'
        isValid = false
      } else if (formData.message.trim().length < 10) {
        errors.message = 'Die Nachricht muss mindestens 10 Zeichen lang sein.'
        isValid = false
      }

      return isValid
    }

    const clearError = (field) => {
      errors[field] = ''
    }

    const closeModal = () => {
      emit('close')
    }

    const handleSubmit = async () => {
      if (!validateForm()) {
        // Find first error field and focus it
        const firstErrorField = Object.keys(errors).find(key => errors[key])
        if (firstErrorField) {
          const element = document.getElementById(`contact-${firstErrorField}`)
          if (element) {
            element.focus()
          }
        }
        return
      }

      isSubmitting.value = true

      // Simulate API call
      await new Promise(resolve => setTimeout(resolve, 1500))

      // Show success message
      showSuccess.value = true
      isSubmitting.value = false

      // Reset form
      formData.name = ''
      formData.email = ''
      formData.subject = ''
      formData.message = ''

      // Close modal after 3 seconds
      setTimeout(() => {
        showSuccess.value = false
        closeModal()
      }, 3000)
    }

    return {
      formData,
      errors,
      isSubmitting,
      showSuccess,
      clearError,
      closeModal,
      handleSubmit
    }
  }
}
</script>
