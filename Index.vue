<template>
  <div class="min-h-screen bg-gray-50">
    <!-- Header -->
    <header class="bg-white shadow-sm border-b border-gray-200">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-4">
        <div class="flex items-center justify-center">
          <div class="flex items-center gap-3">
            <span class="text-3xl medical-icon">🏥</span>
            <h1 class="text-2xl sm:text-3xl font-bold text-red-600 emergency-header text-center">
              MedAlert AI – Emergency Medical Assistant
            </h1>
          </div>
        </div>
        <p class="text-center text-gray-600 text-sm mt-2">
          AI-powered emergency medical assessment and guidance
        </p>
      </div>
    </header>

    <!-- Main Content -->
    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6">
      <!-- Emergency Form Section -->
      <div class="mb-8">
        <EmergencyForm />
      </div>

      <!-- Results Section -->
      <div v-if="medicalStore.hasResults || medicalStore.loading.overall" class="space-y-6">
        <!-- Results Header -->
        <div class="text-center mb-6">
          <h2 class="text-xl font-semibold text-gray-800 mb-2">
            Emergency Assessment Results
          </h2>
          <div v-if="medicalStore.loading.overall" class="flex items-center justify-center gap-2 text-gray-600">
            <ProgressSpinner style="width: 20px; height: 20px" strokeWidth="4" />
            <span class="text-sm">Analyzing emergency situation...</span>
          </div>
        </div>

        <!-- Results Grid -->
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
          <!-- Medical Assessment Card -->
          <div class="order-1">
            <MedicalAssessmentCard />
          </div>

          <!-- Emergency Action Card -->
          <div class="order-2">
            <EmergencyActionCard />
          </div>

          <!-- Nearest Hospital Card -->
          <div class="order-3">
            <NearestHospitalCard />
          </div>

          <!-- First Aid Card -->
          <div class="order-4">
            <FirstAidCard />
          </div>
        </div>

        <!-- Emergency Status Banner -->
        <div v-if="medicalStore.isEmergency && !medicalStore.loading.overall" 
             class="bg-red-100 border-l-4 border-red-500 p-4 rounded-r-lg">
          <div class="flex items-center gap-3">
            <span class="text-2xl">🚨</span>
            <div>
              <h3 class="font-bold text-red-800 text-lg">Emergency Situation Detected</h3>
              <p class="text-red-700 text-sm">
                Based on the assessment, this situation may require immediate medical attention.
                Please follow the emergency action guidance above.
              </p>
            </div>
          </div>
        </div>
      </div>

      <!-- Getting Started Section -->
      <div v-else class="text-center py-12">
        <div class="max-w-2xl mx-auto">
          <div class="text-6xl mb-6">🏥</div>
          <h2 class="text-2xl font-semibold text-gray-800 mb-4">
            Welcome to MedAlert AI
          </h2>
          <p class="text-gray-600 mb-8 leading-relaxed">
            Get instant AI-powered medical assessment and emergency guidance. 
            Fill out the form above with your symptoms and location to receive 
            personalized medical recommendations and find nearby hospitals.
          </p>
          
          <!-- Feature Highlights -->
          <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6 mt-8">
            <div class="bg-white p-4 rounded-lg shadow-sm border border-gray-200">
              <div class="text-2xl mb-2">⚕️</div>
              <h3 class="font-semibold text-gray-800 mb-1">Medical Triage</h3>
              <p class="text-sm text-gray-600">AI assessment of symptom urgency</p>
            </div>
            
            <div class="bg-white p-4 rounded-lg shadow-sm border border-gray-200">
              <div class="text-2xl mb-2">⚡</div>
              <h3 class="font-semibold text-gray-800 mb-1">Emergency Action</h3>
              <p class="text-sm text-gray-600">Immediate response guidance</p>
            </div>
            
            <div class="bg-white p-4 rounded-lg shadow-sm border border-gray-200">
              <div class="text-2xl mb-2">🏥</div>
              <h3 class="font-semibold text-gray-800 mb-1">Hospital Finder</h3>
              <p class="text-sm text-gray-600">Nearest medical facilities</p>
            </div>
            
            <div class="bg-white p-4 rounded-lg shadow-sm border border-gray-200">
              <div class="text-2xl mb-2">🩹</div>
              <h3 class="font-semibold text-gray-800 mb-1">First Aid</h3>
              <p class="text-sm text-gray-600">Step-by-step instructions</p>
            </div>
          </div>
        </div>
      </div>

      <!-- Disclaimer -->
      <div class="mt-12 bg-yellow-50 border border-yellow-200 rounded-lg p-4">
        <div class="flex items-start gap-3">
          <span class="text-yellow-600 text-xl flex-shrink-0">⚠️</span>
          <div class="text-sm text-yellow-800">
            <h4 class="font-semibold mb-1">Medical Disclaimer</h4>
            <p class="leading-relaxed">
              MedAlert AI provides general medical information and guidance for educational purposes only. 
              This is not a substitute for professional medical advice, diagnosis, or treatment. 
              Always seek the advice of qualified healthcare providers with any questions about medical conditions. 
              In case of emergency, call 911 immediately.
            </p>
          </div>
        </div>
      </div>
    </main>

    <!-- Floating SOS Button -->
    <SOSButton />

    <!-- Toast for notifications -->
    <Toast position="top-center" />
  </div>
</template>

<script setup>
import { onMounted } from 'vue'
import { useMedicalStore } from './stores/medicalStore.js'
import EmergencyForm from './components/EmergencyForm.vue'
import MedicalAssessmentCard from './components/MedicalAssessmentCard.vue'
import EmergencyActionCard from './components/EmergencyActionCard.vue'
import NearestHospitalCard from './components/NearestHospitalCard.vue'
import FirstAidCard from './components/FirstAidCard.vue'
import SOSButton from './components/SOSButton.vue'
import ProgressSpinner from 'primevue/progressspinner'
import Toast from 'primevue/toast'

// Initialize store
const medicalStore = useMedicalStore()

// Lifecycle hooks
onMounted(() => {
  // Clear any previous results on page load
  medicalStore.clearResults()
  
  // Set up keyboard shortcuts for accessibility
  const handleKeyboardShortcuts = (event) => {
    // Alt + F for focus on form
    if (event.altKey && event.key === 'f') {
      event.preventDefault()
      const symptomsField = document.getElementById('symptoms')
      if (symptomsField) {
        symptomsField.focus()
      }
    }
    
    // Alt + R for results section
    if (event.altKey && event.key === 'r') {
      event.preventDefault()
      const resultsSection = document.querySelector('.results-section')
      if (resultsSection) {
        resultsSection.scrollIntoView({ behavior: 'smooth' })
      }
    }
  }
  
  document.addEventListener('keydown', handleKeyboardShortcuts)
  
  // Cleanup
  return () => {
    document.removeEventListener('keydown', handleKeyboardShortcuts)
  }
})
</script>

<style scoped>
/* Import main CSS */
@import './main.css';

/* Component-specific styles */
.medical-icon {
  filter: drop-shadow(0 2px 4px rgba(0, 0, 0, 0.1));
}

/* Responsive grid adjustments */
@media (max-width: 1024px) {
  .grid-cols-1.lg\\:grid-cols-2 > div {
    width: 100%;
  }
}

/* Enhanced focus indicators for accessibility */
.emergency-form:focus-within {
  outline: 2px solid var(--emergency-red);
  outline-offset: 4px;
  border-radius: var(--emergency-border-radius);
}

/* Loading state animations */
.results-loading {
  animation: pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
}

@keyframes pulse {
  0%, 100% {
    opacity: 1;
  }
  50% {
    opacity: 0.5;
  }
}

/* High contrast mode support */
@media (prefers-contrast: high) {
  .bg-gray-50 {
    background-color: #ffffff;
  }
  
  .border-gray-200 {
    border-color: #000000;
  }
  
  .text-gray-600 {
    color: #000000;
  }
}

/* Reduced motion support */
@media (prefers-reduced-motion: reduce) {
  .results-loading {
    animation: none;
  }
  
  * {
    transition: none !important;
    animation: none !important;
  }
}

/* Print styles */
@media print {
  .floating-sos-button {
    display: none;
  }
  
  .bg-gray-50 {
    background: white !important;
  }
  
  .shadow-sm {
    box-shadow: none !important;
    border: 1px solid #000 !important;
  }
  
  .emergency-header {
    color: #000 !important;
  }
}

/* Mobile-first responsive design */
@media (max-width: 640px) {
  .emergency-header {
    font-size: 1.5rem;
    line-height: 1.2;
  }
  
  .grid {
    gap: 1rem;
  }
  
  .px-4 {
    padding-left: 1rem;
    padding-right: 1rem;
  }
}

/* Large screen optimizations */
@media (min-width: 1280px) {
  .max-w-7xl {
    max-width: 1200px;
  }
}

/* Focus management for screen readers */
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}

/* Skip link for accessibility */
.skip-link {
  position: absolute;
  top: -40px;
  left: 6px;
  background: var(--emergency-red);
  color: white;
  padding: 8px;
  text-decoration: none;
  border-radius: 4px;
  z-index: 1000;
}

.skip-link:focus {
  top: 6px;
}
</style>