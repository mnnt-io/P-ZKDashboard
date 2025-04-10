# Andrometa Dashboard

![Andrometa Logo](/assets/images/logo.png)

Andrometa Dashboard is a comprehensive platform for managing SHRD tokens, enabling users to track investments, monitor token distribution, and participate in farming opportunities. The dashboard provides a unified interface for token holders and investors.

![Andrometa Dashboard](/assets/images/preview.png)

## 🚀 Features

-   **Token Price Tracking**: Real-time and historical price charts for SHRD tokens
-   **Distribution Analytics**: Detailed daily distribution metrics and visualizations
-   **Farming**: Stake your tokens to earn rewards through various strategies
-   **Treasury Management**: View treasury statistics and holdings
-   **Vesting Plans**: Track token vesting schedules and releases
-   **Wallet Integration**: Connect with Web3Modal for seamless wallet connectivity
-   **Dark/Light Mode**: Toggle between themes for optimal viewing experience

## 🔧 Tech Stack

-   **Frontend**: React.js, TypeScript
-   **Styling**: Tailwind CSS
-   **Charting**: TradingView
-   **Authentication**: Wallet Authentication for users / API_Key for API

## 🛠️ Setup & Installation

### Prerequisites

-   Node.js 16+
-   npm or yarn
-   Web3 wallet for future blockchain integrations

### Installation

1. Clone the repository

```bash
git clone https://github.com/yourusername/zkdashboard.git
cd zkdashboard
```

2. Install dependencies

```bash
npm install
# or
yarn install
```

3. Create a `.env.local` file in the root directory with the following variables:

```
API_KEY=your_api_key
API_URL=https://api.andrometa.gg/v1
```

4. Start the development server

```bash
npm run dev
# or
yarn dev
```

5. Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

## 🔍 Key Components

### Dashboard Sections

The dashboard includes these main sections:

-   **Overview**: Portfolio snapshot and market overview
-   **Farm**: Token staking and reward tracking
-   **Marketplace**: Browse and manage SHRD token assets
-   **Treasury**: View treasury holdings and metrics

### BSC

BSC is currently proof of concepts for potential future partnerships.

### Token Management

The dashboard supports these token management functions:

-   Viewing token price and distribution data
-   Tracking personal holdings
-   Managing farm positions
-   Monitoring vesting plans

## 📝 API Integration

The platform communicates with a backend API at `https://api.andrometa.gg/v1` (![Documentation](/API-Docs.md)) which provides:

-   SHRD token price data
-   Distribution analytics
-   User holdings information
-   Farm position data
-   Treasury statistics
-   Vesting plan details

## Future Plans

The platform is currently implemented as an off-chain solution with plans to integrate with Skale blockchain in future updates.
