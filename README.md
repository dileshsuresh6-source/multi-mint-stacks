# 🎨 Stacksies NFT Contract

Deployed Contract Address:
ST87DZSKM3M2NR2EB6G25ZP13GW9Q25026D24VEJ.multi-mint

📜 Project Title & Short Description

Stacksies NFT Contract (Stacks / Clarity)

This smart contract implements a non-fungible token (NFT) collection called Stacksies on the Stacks blockchain.
It follows the SIP-009 NFT standard and provides secure minting, transfers, and a multi-mint airdrop mechanism for large-scale distributions.

🛠 Tech Stack Used

Blockchain: Stacks

Language: Clarity

Framework: Clarinet (for local testing & deployment)

Explorer: Hiro Explorer (for testnet/mainnet interactions)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/fd875174-ab09-4465-b988-5c825bde8c35" />


⚙️ Setup Instructions
Local (Clarinet)
clarinet new stacksies
cd stacksies

# Replace contract file
clarinet check
clarinet console

Testnet/Mainnet

Deploy via Stacks CLI or Clarinet.

Open in Hiro Explorer to interact with the contract.

📦 Smart Contract Functions
Read-Only Functions

get-last-token-id → (ok uint) → Returns the most recent token ID.

get-token-uri (token-id uint) → Metadata URI (currently none).

get-owner (token-id uint) → Returns the owner of a token.

Public Functions

mint (recipient principal) → Mints a new NFT to recipient (owner-only).

transfer (token-id uint) (sender principal) (recipient principal) → Transfers token with ownership validation.

multi-mint (airdrop1 list, airdrop2 list, airdrop3 list, start-last-token-id uint) → Batch mint to up to ~14,996 addresses.

🚀 How to Use the Project

Mint a Single NFT

(contract-call? .stacksies mint 'ST123...ABC)


Transfer an NFT

(contract-call? .stacksies transfer u1 tx-sender 'ST456...XYZ)


Batch Airdrop / Multi-Mint

(contract-call? .stacksies multi-mint
(list 'ST123...AAA 'ST123...BBB)
(list 'ST123...CCC)
(list)
u0
)

⭐ Features

✅ SIP-009 compliant (nft-trait)

✅ Owner-only minting

✅ NFT transfers with validation

✅ Multi-mint airdrop (up to ~14,996 addresses)

✅ Track last minted token ID

✅ On-chain read-only metadata

⚠️ Error Codes

u100 → err-owner-only → Only contract owner may act.

u101 → err-not-token-owner → Caller is not the token owner.
