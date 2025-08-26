FarmBlock Smart Contracts
Overview
Welcome to the FarmBlock Smart Contracts repository! This repository contains the Solidity smart contracts powering the FarmBlock decentralized application (DApp), integrated with the MiniPay template for a seamless user experience on the Celo blockchain. FarmBlock leverages self-sovereign zero-knowledge proofs (zkP) to enable privacy-preserving authentication and other features, enhancing security and user control.
The contracts are designed to interact with the FarmBlock front-end (farmblock-app), a Next.js-based monorepo hosted at https://github.com/oforgee007/farmblock-app. This README provides setup instructions, contract details, deployment guidelines, and contribution information.
Table of Contents
	•	Overview  
	•	Features  
	•	Prerequisites  
	•	Project Structure  
	•	Installation  
	•	Contract Details  
	•	Deployment  
	•	Interacting with the DApp  
	•	Testing  
	•	Contributing  
	•	License  
	•	Contact  
Features
	•	zkP Authentication: Supports self-sovereign zero-knowledge proofs for user verification (e.g., age > 18) without revealing personal data.  
	•	Wallet Integration: Compatible with WalletConnect and MetaMask for secure wallet connections via the FarmBlock front-end.  
	•	Celo Blockchain: Deployed on the Alfajores testnet, with potential for mainnet migration.  
	•	Modular Design: Contracts are structured for extensibility, supporting future features like farming rewards or governance.  
Prerequisites
Before setting up the smart contracts, ensure you have the following installed:
	•	Node.js: Version 18.x or 20.x LTS (download from nodejs.org).  
	•	Hardhat: Ethereum development environment (npm install -g hardhat).  
	•	Foundry (optional): Alternative for testing and deployment (curl -L https://foundry.paradigm.xyz | bash).  
	•	MetaMask: For managing testnet accounts and deploying contracts.  
	•	Celo CLI: For interacting with the Celo network (npm install -g @celo/celo-cli).  
	•	Git: For cloning the repository.  
	•	npm or pnpm: Package manager (npm recommended for consistency with the FarmBlock monorepo).  
Project Structure
farmblock-contracts/
├── contracts/           # Solidity smart contracts
│   ├── ZkpAuth.sol     # zkP authentication contract
│   ├── FarmBlock.sol   # Main contract for FarmBlock logic
│   └── ...             # Additional contracts
├── scripts/            # Deployment scripts
│   ├── deploy.ts       # Hardhat deployment script
│   └── ...             # Other scripts
├── test/               # Test files
│   ├── ZkpAuth.test.js # Hardhat tests
│   └── ...             # Additional tests
├── hardhat.config.js   # Hardhat configuration
├── package.json        # Project dependencies
├── .gitignore          # Git ignore file
└── README.md           # This file

	•	contracts/: Contains the core Solidity files.  
	•	scripts/: Includes deployment and interaction scripts.  
	•	test/: Houses unit and integration tests.  
	•	hardhat.config.js: Configures Hardhat for compilation and deployment.  
Installation
Clone the Repository   git clone https://github.com/oforgee007/farmblock-contracts.git
cd farmblock-contracts
	1	
Install Dependencies   npm install
	2	
	3	Configure Environment Variables  
Create a .env file in the root directory:   PRIVATE_KEY=your_private_key_for_deployment
ALFAJORES_RPC_URL=https://alfajores-forno.celo-testnet.org
	•	
	•	Obtain a private key from MetaMask (use a test account) and an RPC URL from Celo documentation.  
Contract Details
ZkpAuth.sol
	•	Purpose: Handles zkP verification for user authentication.  
	•	Key Functions:  
	◦	verifyProof(bytes memory proof, uint256[2] memory publicSignals): Verifies a zero-knowledge proof.  
	◦	registerUser(address user): Registers a user post-verification.  
	•	Events:  
	◦	UserRegistered(address user, uint256 timestamp): Emitted on successful registration.  
FarmBlock.sol
	•	Purpose: Manages core FarmBlock logic (e.g., farming rewards, user data).  
	•	Key Functions:  
	◦	stake(uint256 amount): Allows users to stake tokens.  
	◦	claimRewards(): Claims accumulated rewards.  
	•	Storage:  
	◦	mapping(address => uint256) public stakes: Tracks user stakes.  
	•	Events:  
	◦	Staked(address user, uint256 amount): Emitted on staking.  
(Note: Adjust contract names and functions based on your actual implementation. Share details if you want specifics included.)
Deployment
Compile Contracts   npx hardhat compile
	1	
	2	Deploy to Alfajores  
	◦	Ensure MetaMask is set to the Alfajores testnet.  
Run the deployment script:   npx hardhat run scripts/deploy.ts --network alfajores
	•	
	•	The script outputs contract addresses (e.g., save ZkpAuth and FarmBlock addresses).  
	3	Verify on Celo Explorer  
	◦	Use the Celo Explorer (https://explorer.celo.org/alfajores) to verify contracts by providing the source code and address.  
Interacting with the DApp
	•	The FarmBlock front-end (farmblock-app) interacts with these contracts via Wagmi hooks (e.g., useContractRead, useContractWrite).  
Update lib/wagmi.ts in the front-end with contract ABIs and addresses:   import { createConfig } from 'wagmi';
import { alfajores } from 'wagmi/chains';
import { ZkpAuthABI, FarmBlockABI } from './abis'; // Add ABI files

export const wagmiConfig = createConfig({
  chains: [alfajores],
  // ... other config
  contracts: {
    ZkpAuth: {
      address: '0xYourZkpAuthAddress',
      abi: ZkpAuthABI,
    },
    FarmBlock: {
      address: '0xYourFarmBlockAddress',
      abi: FarmBlockABI,
    },
  },
});
	•	
	•	Test interactions (e.g., zkP verification) on http://localhost:3000.  
Testing
Run Tests   npx hardhat test
	1	
	◦	Ensure tests cover zkP verification and core functions.  
	2	Add Test Cases  
	◦	Extend test/ZkpAuth.test.js with scenarios for invalid proofs or edge cases.  
Contributing
	1	Fork the repository.  
	2	Create a branch: git checkout -b feature/your-feature.  
	3	Commit changes: git commit -m "Add your feature".  
	4	Push to the branch: git push origin feature/your-feature.  
	5	Open a Pull Request.  
License
This project is licensed under the MIT License - see the LICENSE file for details.
Contact
	•	Author: Jordan Oforge jordan.ofurum@gmail.com  
	•	GitHub: https://github.com/oforgee007  
Issues: Report bugs or suggestions at Issues.
