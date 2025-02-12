<script setup>
import { ref, onMounted } from 'vue'
import BusinessDescriptionCard from './components/BusinessDescriptionCard.vue'
import BusinessOverviewCard from './components/BusinessOverviewCard.vue'
import ProductServiceCard from './components/ProductServiceCard.vue'
import RiskFactorCard from './components/RiskFactorCard.vue'
import FuturePlanCard from './components/FuturePlanCard.vue'
import SectionContainer from './components/SectionContainer.vue'

import AAPL from './contents/AAPL.json'
import FIX from './contents/FIX.json'
import LULU from './contents/LULU.json'
import MSFT from './contents/MSFT.json'
import NFLX from './contents/NFLX.json'
import RL from './contents/RL.json'
import TTEK from './contents/TTEK.json'

const companies = ['AAPL', 'FIX', 'LULU', 'MSFT', 'NFLX', 'RL', 'TTEK']
const selectedCompany = ref(null)
const companyData = ref(null)

const companyDataMap = {
  AAPL,
  FIX,
  LULU,
  MSFT,
  NFLX,
  RL,
  TTEK
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
          <div class="flex flex-wrap gap-2 justify-end">
            <button
              v-for="company in companies"
              :key="company"
              @click="loadCompanyData(company)"
              :class="[
                'px-4 py-2 rounded-lg font-semibold transition-all duration-200 hover:shadow-md',
                selectedCompany === company
                  ? 'bg-blue-900 text-white shadow-md transform scale-105'
                  : 'bg-gray-800 text-gray-300 hover:bg-gray-700 hover:text-white border border-gray-700'
              ]"
            >
              {{ company }}
            </button>
          </div>
        </div>
      </div>
    </nav>

    <div class="container mx-auto px-4 py-8 max-w-7xl">
      <div v-if="companyData">
        <h1 class="text-4xl font-bold text-gray-900 mb-8">{{ companyData.symbol }} - Company Information</h1>

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
