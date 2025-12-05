<template>
  <div class="min-h-screen">
    <HeroSection 
      :currentAmount="totalDonations" 
      :goalAmount="goalAmount"
    />
    <DonationForm 
      @donation-submitted="handleDonation"
    />
    <FaqSection 
      @open-contact="openContactModal"
    />
    
    <!-- Footer -->
    <footer class="bg-gray-900 text-white py-8 px-6">
      <div class="max-w-4xl mx-auto text-center">
        <p class="text-gray-400 text-sm">
          &copy; 2025 Hilfsorganisation. Alle Rechte vorbehalten.
        </p>
        <p class="text-gray-500 text-xs mt-2">
          Dies ist eine fiktive Spenden-Landingpage für Demonstrationszwecke.
        </p>
      </div>
    </footer>

    <!-- Thank You Modal -->
    <ThankYouModal 
      :show="showThankYouModal"
      :amount="donatedAmount"
      @close="closeThankYouModal"
    />

    <!-- Contact Modal -->
    <ContactModal 
      :show="showContactModal"
      @close="closeContactModal"
    />
  </div>
</template>

<script>
import { ref } from 'vue'
import HeroSection from './components/HeroSection.vue'
import DonationForm from './components/DonationForm.vue'
import FaqSection from './components/FaqSection.vue'
import ThankYouModal from './components/ThankYouModal.vue'
import ContactModal from './components/ContactModal.vue'

export default {
  name: 'App',
  components: {
    HeroSection,
    DonationForm,
    FaqSection,
    ThankYouModal,
    ContactModal
  },
  setup() {
    const totalDonations = ref(4200)
    const goalAmount = ref(10000)
    const showThankYouModal = ref(false)
    const showContactModal = ref(false)
    const donatedAmount = ref(0)

    const handleDonation = (amount) => {
      totalDonations.value += amount
      donatedAmount.value = amount
      showThankYouModal.value = true
      
      // Scroll to top to see updated barometer
      window.scrollTo({ top: 0, behavior: 'smooth' })
    }

    const closeThankYouModal = () => {
      showThankYouModal.value = false
    }

    const openContactModal = () => {
      showContactModal.value = true
    }

    const closeContactModal = () => {
      showContactModal.value = false
    }

    return {
      totalDonations,
      goalAmount,
      showThankYouModal,
      showContactModal,
      donatedAmount,
      handleDonation,
      closeThankYouModal,
      openContactModal,
      closeContactModal
    }
  }
}
</script>
