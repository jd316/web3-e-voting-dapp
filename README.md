# Web3-e-Voting-Dapp

This project is a web-based, blockchain-powered voting system built on Ethereum. It consists of two main modules—an Election Commission (EC) interface for administrators to set up and manage elections, and a voter interface that lets registered users authenticate with their Ethereum wallets and cast votes securely via a decentralized application (DApp).

## Features

- Decentralized voting on a private or public Ethereum network
- Secure voter authentication via Ethereum wallet (e.g., MetaMask)
- Election Commission dashboard to create elections, add candidates and voters, and control the election lifecycle
- Immutable vote recording through smart contracts
- Real-time vote tallying and transparent results


## Architecture

This DApp uses a typical client–server pattern augmented by blockchain:

- **Smart Contracts**
    - Election contract handles voter registration, candidate management, vote casting, and result calculation.
- **Backend / Node Server**
    - Facilitates deployment and interaction with the smart contract, handles off-chain configuration, and secures administrator actions.
- **Frontend (Client)**
    - A web interface built with React (or similar) that connects to users’ wallets via Web3.js or Ethers.js.


## Tech Stack

- Solidity for smart contracts
- Ethereum (Ganache for local development or any test/public network)
- Node.js + Express (or similar) for backend APIs
- React (or another JS framework) for frontend
- Web3.js or Ethers.js for blockchain integration
- Truffle or Hardhat for contract compilation and migration


## Prerequisites

- Node.js (v14+) and npm or Yarn
- Ganache (for local blockchain) or access to an Ethereum testnet/mainnet
- MetaMask or any compatible Web3 wallet extension


## Installation

1. Clone the repo

```bash
git clone https://github.com/jd316/web3-e-voting-dapp.git
cd web3-e-voting-dapp
```

2. Install dependencies

```bash
npm install
# or
yarn install
```

3. Configure environment
    - Copy `.env.example` to `.env` and set:

```ini
RPC_URL=http://127.0.0.1:7545        # Ganache or Infura endpoint
PRIVATE_KEY=your_admin_wallet_key   # For contract deployment
CONTRACT_ADDRESS=                   # (Populated after migration)
```

4. Compile and deploy smart contracts

```bash
npx truffle compile
npx truffle migrate --network development
```

5. Frontend setup

```bash
cd client
npm start
# or
yarn start
```

Visit http://localhost:3000 in your browser.

## Usage

**For Administrators (Election Commission)**

- Connect your Ethereum wallet with the admin account.
- Create a new election by specifying a name, description, and timeline.
- Register candidates and authorize voter addresses.
- Start and end the election via the EC dashboard.

**For Voters**

- Install MetaMask and connect to the same network as the smart contract.
- Navigate to the voter interface, connect your wallet, and confirm your registered address.
- Cast your vote by selecting a candidate; the transaction is submitted on-chain.


## Smart Contract Overview

```solidity
contract Election {
  struct Voter {
    bool authorized;
    bool voted;
    uint voteIndex;
  }
  struct Candidate {
    string name;
    uint voteCount;
  }

  address public admin;
  mapping(address => Voter) public voters;
  Candidate[] public candidates;
  bool public electionActive;

  // Events: VoterAuthorized, VoteCast, ElectionStarted, ElectionEnded
  // Functions: authorizeVoter, addCandidate, startElection, stopElection, vote, getResults
}
```


## Future Enhancements

- Integrate biometric verification or decentralized identity (DID) systems
- Support multi-constituency and multi-phase elections
- Add zero-knowledge proofs for enhanced voter privacy
- Deploy on production-grade Ethereum layer-2 networks for scalability


## License

This project is released under the MIT License. Feel free to fork, modify, and contribute!
