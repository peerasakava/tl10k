<script setup>
import { ref, onMounted } from 'vue'
import BusinessDescriptionCard from './components/BusinessDescriptionCard.vue'
import BusinessOverviewCard from './components/BusinessOverviewCard.vue'
import ProductServiceCard from './components/ProductServiceCard.vue'
import RiskFactorCard from './components/RiskFactorCard.vue'
import FuturePlanCard from './components/FuturePlanCard.vue'
import SectionContainer from './components/SectionContainer.vue'

// Import all company data files
import AAPL from './contents/AAPL.json'
import AMAL from './contents/AMAL.json'
import ATGE from './contents/ATGE.json'
import CPRX from './contents/CPRX.json'
import FIX from './contents/FIX.json'
import IDCC from './contents/IDCC.json'
import JPM from './contents/JPM.json'
import LULU from './contents/LULU.json'
import META from './contents/META.json'
import MSFT from './contents/MSFT.json'
import NFLX from './contents/NFLX.json'
import RL from './contents/RL.json'
import TSLA from './contents/TSLA.json'
import TTEK from './contents/TTEK.json'

const companies = [
  'AAPL', 'AMAL', 'ATGE', 'CPRX', 'FIX', 'IDCC', 'JPM',
  'LULU', 'META', 'MSFT', 'NFLX', 'RL', 'TSLA', 'TTEK'
]
const selectedCompany = ref(null)
const companyData = ref(null)

const companyDataMap = {
  AAPL, AMAL, ATGE, CPRX, FIX, IDCC, JPM,
  LULU, META, MSFT, NFLX, RL, TSLA, TTEK
}

const loadCompanyData = (symbol) => {
  selectedCompany.value = symbol
  companyData.value = companyDataMap[symbol]
}

onMounted(() => {
  if (companies.length > 0) {
    loadCompanyData(companies[0])
  }
})
</script>

<template>
  <div>
    <!-- Company Navigation Bar -->
    <nav class="bg-gray-900 shadow-lg sticky top-0 z-50 w-full">
      <div class="container mx-auto px-4 py-4">
        <div class="flex items-center justify-between">
          <h1 class="text-2xl font-bold text-white">tl10k</h1>
          <div class="relative w-48">
            <select
              v-model="selectedCompany"
              @change="loadCompanyData($event.target.value)"
              class="w-full px-4 py-2 bg-gray-800 text-white rounded-lg appearance-none cursor-pointer focus:outline-none focus:ring-2 focus:ring-blue-500 border border-gray-700"
            >
              <option v-for="company in companies" :key="company" :value="company">
                {{ company }}
              </option>
            </select>
            <div class="absolute inset-y-0 right-0 flex items-center px-2 pointer-events-none">
              <svg class="w-4 h-4 text-gray-400" viewBox="0 0 20 20" fill="currentColor">
                <path fill-rule="evenodd" d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z" clip-rule="evenodd" />
              </svg>
            </div>
          </div>
        </div>
      </div>
    </nav>

    <div class="container mx-auto px-4 py-8 max-w-7xl">
      <div v-if="companyData">
        <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4 sm:gap-8 mb-8">
          <h1 class="text-3xl sm:text-4xl font-bold text-gray-900">{{ companyData.symbol }} - Company Information</h1>
          <a 
            :href="companyData.filing_url" 
            target="_blank" 
            rel="noopener noreferrer" 
            class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors duration-200 font-semibold flex items-center gap-2 whitespace-nowrap"
          >
            <span>Read Full 10-K</span>
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
              <path d="M11 3a1 1 0 100 2h2.586l-6.293 6.293a1 1 0 101.414 1.414L15 6.414V9a1 1 0 102 0V4a1 1 0 00-1-1h-5z" />
              <path d="M5 5a2 2 0 00-2 2v8a2 2 0 002 2h8a2 2 0 002-2v-3a1 1 0 10-2 0v3H5V7h3a1 1 0 000-2H5z" />
            </svg>
          </a>
        </div>

        <!-- Main Content Grid -->
        <!-- Business Overview Section -->
        <SectionContainer title="Business Overview">
          <BusinessDescriptionCard
            :description="companyData.business_overview.business_description"
            class="xl:col-span-3"
          />

          <BusinessOverviewCard
            title="Revenue Model"
            icon="💰"
            :content="companyData.business_overview.revenue_model"
          />

          <BusinessOverviewCard
            title="Strategic Direction"
            icon="🎯"
            :content="companyData.business_overview.strategic_direction"
          />

          <BusinessOverviewCard
            title="Long Term Goals"
            icon="🌟"
            :content="companyData.business_overview.long_term_goals"
          />
        </SectionContainer>

        <!-- Products and Services Section -->
        <SectionContainer title="Products and Services">
          <template v-for="(product, index) in companyData.products_and_services" :key="index">
            <ProductServiceCard
              :name="product.product_service_name"
              :summary="product.summary"
              :details="product.details"
            />
          </template>
        </SectionContainer>

        <!-- Risk Factors Section -->
        <SectionContainer title="Risk Factors">
          <template v-for="(risk, index) in companyData.risk_factors" :key="index">
            <RiskFactorCard
              :title="risk.risk_factor_title"
              :summary="risk.summary"
              :details="risk.details"
            />
          </template>
        </SectionContainer>

        <!-- Future Plans Section -->
        <SectionContainer title="Strategies and Future Plans">
          <template v-for="(plan, index) in companyData.strategies_and_future_plans" :key="index">
            <FuturePlanCard
              :headline="plan.future_strategy_focus_headline"
              :summary="plan.summary"
              :management-quote="plan.management_quote"
            />
          </template>
        </SectionContainer>
      </div>
      <div v-else>
        <p class="text-gray-600 text-lg">Loading company data...</p>
      </div>
    </div>
  </div>
</template>
