# tl10k-web-vite

A modern web application built with Vue.js and Vite that displays comprehensive company information extracted from 10-K filings. The application provides an interactive interface to explore business overviews, products/services, risk factors, and future strategies of various companies.

## Features

- 📊 Interactive company selection navigation
- 💼 Detailed business overview sections
- 🏭 Products and services information
- ⚠️ Risk factors analysis
- 🎯 Future strategies and plans
- 📄 Direct links to full 10-K filings
- 🎨 Modern, responsive UI with Tailwind CSS

## Project Structure

```
src/
├── components/           # Vue components
│   ├── BusinessDescriptionCard.vue
│   ├── BusinessOverviewCard.vue
│   ├── FuturePlanCard.vue
│   ├── ProductServiceCard.vue
│   ├── RiskFactorCard.vue
│   └── SectionContainer.vue
├── contents/            # JSON data files for companies
└── App.vue             # Main application component
```

## Setup

1. Install dependencies:
```bash
bun install
```

2. Run development server:
```bash
bun run dev
```

3. Build for production:
```bash
bun run build
```

## Technology Stack

- **Framework**: Vue.js 3
- **Build Tool**: Vite
- **Runtime**: Bun
- **Styling**: Tailwind CSS
- **Data Format**: JSON

## Data Structure

Company data is stored in JSON format in the `/contents` directory. Each company file contains structured information about:

- Business Overview
- Products and Services
- Risk Factors
- Strategies and Future Plans
- Filing URLs

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is proprietary software. All rights reserved.
