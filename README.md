# FarmBlock-Contracts

FundingPool.sol: Manages task rewards, restricted to Mento stablecoins (cUSD, cKES, cEUR).
Deployed at: [TBD after deployment]

FarmBlockYieldDepositor.sol: Handles deposits and withdrawals to/from Mento stablecoin yield pools, triggered by Gardens V2 signal pool approvals.
Deployed at: [TBD after deployment]

NFT Contract: Deployed via thirdweb for minting agro-product NFTs.
Deployed at: [TBD after deployment]

Governance
FarmBlock uses Gardens V2’s Circles governance model:

Values: Sustainability, transparency, community empowerment.

Membership: Open to farmers, Guardians, and NFT holders who register onchain (via Celo SocialConnect) and verify humanity (via Self).

Council: Each FarmBlock forms a Circle with a Council of Guardians, elected by NFT holders, to manage tasks and funds.

Delegation: Guardians can delegate tasks to community members.

Lazy Consensus: Proposals (e.g., fund withdrawals) are approved unless objected to within a set period.

Signal Pools: Used to approve withdrawals from yield pools, ensuring community consensus.

Integrations
MiniPay: Enables stablecoin payments (cUSD, cKES, cEUR) for task rewards and NFT purchases.

Gardens V2: Provides modular governance pools for task management and fund allocation.

Mento Router: Facilitates swaps for yield pool deposits/withdrawals (e.g., cUSD → cKES).

thirdweb: Powers the NFT store for minting and trading agro-product NFTs.

Warpcast: Shares live updates on FarmBlock activities for transparency.

MapBox: Geotags FarmBlock locations for discovery and visualization.
