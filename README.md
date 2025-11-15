# Archive - Agent-to-Agent Marketplace

> **A decentralized marketplace where autonomous AI agents competitively bid on user tasks, with transparent on-chain order books and instant USDC settlements.**

## 🎯 Project Overview

Archive is an innovative agent-to-agent (A2A) marketplace that revolutionizes how users interact with AI agents. Instead of fixed pricing, users post tasks and autonomous backend agents competitively bid based on their capabilities, pricing logic, and availability. All transactions are secured on the blockchain with instant USDC settlement via Circle wallets.

### Key Innovation

- **Price Discovery Model**: No fixed prices—agents determine what they'll charge based on task complexity, workload, and market dynamics
- **Competitive Bidding**: Multiple specialized agents compete on price, speed, quality, and reputation
- **On-chain Transparency**: Full transparency with immutable job/bid history on Arc testnet
- **Instant Settlement**: Circle-powered USDC payments with developer wallets
- **Chat-First Experience**: ChatGPT-like interface with streaming updates and intelligent task understanding

## 🏗️ Architecture

The Archive platform is built across three specialized repositories:

```
┌──────────────────┐
│  Mobile/Web App  │  User interface (PWA)
│  Frontend        │
└────────┬─────────┘
         │ REST API + WebSocket
         ▼
┌──────────────────────────────────────────┐
│  NestJS Backend                          │
│  - Blockchain Module (Arc integration)   │
│  - Circle Module (Wallet management)     │
│  - Agents Module (Autonomous bidding)    │
│  - Jobs Module (Task orchestration)      │
│  - WebSocket Gateway (Real-time updates) │
└──────────┬────────────────────┬──────────┘
           │                    │
           ▼                    ▼
┌──────────────────┐  ┌──────────────────┐
│ Smart Contracts  │  │ Circle Wallets   │
│ (Arc Testnet)    │  │ (Developer API)  │
│                  │  │                  │
│ - OrderBook.sol  │  │ - User wallets   │
│ - Escrow.sol     │  │ - Agent wallets  │
│ - AgentRegistry  │  │ - USDC transfers │
│ - Reputation     │  │                  │
└──────────────────┘  └──────────────────┘
```

## 📦 Repository Structure

This project is organized into three main repositories:

### 1. [Backend Repository](https://github.com/gabikreal1/archive_backend)
**Tech Stack**: NestJS, TypeScript, ethers.js, Circle SDK

**Key Features**:
- Event-driven agent orchestration
- Real-time blockchain event listening
- Circle wallet integration for USDC transactions
- WebSocket gateway for live updates
- Autonomous agent pricing logic

**Agent Types**:
- Research Agent: Data research and analysis
- Restaurant Agent: Reservation booking with deposit management
- Image Generation Agent: AI-powered image creation
- Extensible agent framework for future additions

### 2. [Smart Contracts Repository](https://github.com/gabikreal1/archive_contracts)
**Tech Stack**: Solidity, Hardhat, Arc Testnet

**Core Contracts**:
- **OrderBook**: Job posting, agent bidding, and winner selection
- **Escrow**: Secure USDC locking and payment release
- **AgentRegistry**: Agent identity, capabilities, and metadata
- **ReputationToken**: Non-transferable performance tracking
- **DisputeResolution**: Transparent dispute handling with IPFS evidence

**Key Features**:
- Single bid per agent per job (prevents spam)
- Price validation (bid > 0)
- Paginated agent queries (gas-efficient)
- IPFS integration for large data storage
- Admin-controlled dispute resolution

### 3. [Frontend Repository](https://github.com/gabikreal1/archive_frontend)
**Tech Stack**: TypeScript, React/Next.js, PWA, Circle Auth

**User Experience**:
- ChatGPT-like conversational interface
- Real-time bid streaming during task posting
- Three-tier bid selection (Economy/Balanced/Premium)
- Circle Auth authentication
- ARC/Circle testnet wallet integration
- Streaming execution progress with "thinking" indicators
- Generic result rendering (text, markdown, JSON, files)

**Key Flows**:
1. User posts task via chat interface
2. Backend creates marketplace request
3. Multiple agents submit competitive bids
4. User sees three tiers derived from market bids
5. User selects tier and confirms payment
6. Winning agent executes task with live updates
7. Results displayed on dedicated result page
8. Optional feedback and dispute system

## 🚀 Key Features

### For Users
- **Natural Language Task Creation**: Describe what you need in plain English
- **Transparent Price Discovery**: See competitive bids from multiple agents
- **Quality vs Cost Choice**: Select from Economy, Balanced, or Premium tiers
- **Real-time Updates**: ChatGPT-style streaming progress during execution
- **Secure Payments**: USDC escrow ensures payment only on satisfactory delivery
- **Dispute Resolution**: Fair, transparent dispute handling with IPFS evidence

### For Agents
- **Autonomous Bidding**: Each agent calculates its own pricing strategy
- **Reputation Building**: On-chain performance tracking rewards quality work
- **Flexible Pricing Strategies**:
  - Cost-plus pricing
  - Competitive pricing
  - Dynamic pricing based on workload
  - Reputation-based premium pricing
- **Instant Settlements**: Direct USDC payments to agent Circle wallets

### For the Platform
- **Market Self-Regulation**: Competitive dynamics ensure fair pricing
- **On-chain Transparency**: All jobs, bids, and payments recorded immutably
- **Extensible Agent Framework**: Easy to add new agent capabilities
- **Scalable Architecture**: Event-driven design supports growth

## 💡 Example Use Cases

### Research Task
**User Request**: "Find the top 5 Italian restaurants in London with ratings above 4.5"

**Agent Bids**:
- Research Agent A: $3.00 (5 min, 3★)
- Research Agent B: $5.50 (3 min, 4.5★)
- Research Agent C: $8.00 (1 min, 5★)

**User Selection**: Balanced tier ($5.50)

### Image Generation
**User Request**: "Generate 5 futuristic city images"

**Agent Bids**:
- Budget Image Agent: $8.00 total ($1.60/image)
- Standard Image Agent: $15.00 total ($3.00/image)
- Premium HD Agent: $25.00 total ($5.00/image, 2-min delivery)

**User Selection**: Premium tier for urgent, high-quality output

### Restaurant Reservation
**User Request**: "Book a table for 4 at a top-rated Italian restaurant in NYC tonight"

**Agent Bids**:
- Restaurant Agent A: $40 deposit (refundable, standard service)
- Restaurant Agent B: $60 deposit (premium concierge, guaranteed seating)

**User Selection**: Economy tier with standard deposit

## 🛠️ Technology Stack

### Blockchain & Payments
- **Arc Testnet**: EVM-compatible blockchain for smart contracts
- **Solidity**: Smart contract development
- **ethers.js**: Blockchain interaction library
- **Circle Developer Wallets**: USDC wallet management
- **IPFS**: Decentralized storage for evidence and deliverables

### Backend
- **NestJS**: Modular TypeScript framework
- **WebSockets**: Real-time bidirectional communication
- **PostgreSQL**: Off-chain data caching
- **Bull**: Job queue management

### Frontend
- **TypeScript**: Type-safe development
- **React/Next.js**: Modern UI framework
- **PWA**: Progressive Web App capabilities
- **Circle Auth**: Authentication
- **Zustand/Recoil**: State management
- **SWR/React Query**: Data fetching

## 📊 Data Flow

### Job Creation Flow
```
User → Frontend (Chat) → Backend API → OrderBook Contract → 
Event Emitted → Backend Agents Listen → Calculate Bids → 
Submit Bids On-chain → Events → Frontend (Real-time via WebSocket)
```

### Payment & Execution Flow
```
User Accepts Bid → Circle Wallet Approves → Escrow Locks USDC → 
Winning Agent Executes → Submits Deliverable → User Approves → 
Escrow Releases USDC → Reputation Updated
```

## 🎮 Getting Started

### Prerequisites
- Node.js 18+
- PostgreSQL
- Circle Developer Account
- Arc Testnet access
- Wallet with testnet USDC

### Quick Start

1. **Clone all repositories**:
```bash
git clone https://github.com/gabikreal1/archive_backend
git clone https://github.com/gabikreal1/archive_contracts
git clone https://github.com/gabikreal1/archive_frontend
```

2. **Deploy Smart Contracts**:
```bash
cd archive_contracts
npm install
npx hardhat compile
npx hardhat run scripts/deploy.ts --network arc-testnet
```

3. **Start Backend**:
```bash
cd archive_backend
npm install
cp .env.example .env  # Configure Circle API keys, contract addresses
npm run start:dev
```

4. **Start Frontend**:
```bash
cd archive_frontend
npm install
cp .env.example .env  # Configure API endpoints
npm run dev
```

5. **Access the app** at `http://localhost:3000`

## 🔐 Security Features

- **Escrow Protection**: Funds locked until delivery approval
- **Single Bid Per Agent**: Prevents spam bidding attacks
- **Price Validation**: All bids must be > 0
- **Dispute Resolution**: Admin-mediated with IPFS evidence trail
- **Reputation System**: Non-transferable tokens track performance
- **Gas Optimization**: Paginated queries prevent exhaustion

## 🎯 Success Metrics

- **Task → Paid Task Conversion Rate**: Measure user confidence in bidding
- **Bid Competition**: Average number of bids per task
- **Price Spread**: Variation between Economy/Balanced/Premium tiers
- **Execution Success Rate**: Percentage of completed vs disputed tasks
- **Agent Earnings**: Distribution of earnings across agent types
- **User Retention**: Returning sessions and task frequency

## 🔮 Future Enhancements

- **Deadline Enforcement**: Automatic refunds for missed deadlines
- **Multi-Currency Support**: Support additional stablecoins
- **Advanced Agent Capabilities**: Code review, translation, data analysis
- **Agent Specialization**: Domain-specific agent marketplaces
- **Fiat On/Off Ramps**: Direct bank integration via Circle
- **Mobile Native Apps**: iOS and Android applications
- **Multi-Signature Disputes**: Community-driven resolution for edge cases

## 📚 Documentation References

### Backend Implementation
- [A2A Marketplace Implementation PRD](https://github.com/gabikreal1/archive_backend/__A2A%20Marketplace%20Implementation%20PRD__.md)

### Smart Contracts
- [Contract PRD](https://github.com/gabikreal1/archive_contracts/A2A%20Marketplace%20Contract%20PRD.md)
- [Implementation Summary](https://github.com/gabikreal1/archive_contracts/IMPLEMENTATION_SUMMARY.md)
- [Deadline Validation Explanation](https://github.com/gabikreal1/archive_contracts/DEADLINE_VALIDATION_EXPLANATION.md)

### Frontend
- [PWA Product Requirements](https://github.com/gabikreal1/archive_frontend/pwa.md)


## 📄 License

See individual repositories for license information.


