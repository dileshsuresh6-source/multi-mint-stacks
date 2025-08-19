Deployed Contract Address = ST2SW0QXQ5AB4ZF5EAHTGMXCKCFF9JHK9GYYBKH9M.multi-mint
🎨 Stacksies NFT Contract (Stacks / Clarity)
📜 Overview

This smart contract implements a non-fungible token (NFT) collection called Stacksies on the Stacks blockchain.

The contract follows the SIP-009 NFT standard
and provides:

Standard NFT ownership and transfer functions.

A secure owner-only minting mechanism.

A multi-mint (airdrop) feature for large batch distributions.
<img width="1920" height="1080" alt="Screenshot from 2025-08-20 01-09-59" src="https://github.com/user-attachments/assets/237447ae-8759-46e7-8185-827f009eb31c" />

⭐ Features

✅ Implements nft-trait for SIP-009 compliance.

✅ Minting restricted to contract owner.

✅ Transfer between users with ownership validation.

✅ Batch Multi-Mint (airdrop up to ~14,996 addresses).

✅ Track last minted token ID.

✅ On-chain read-only functions for metadata and ownership.

⚙️ Error Codes
Code Meaning
u100 → err-owner-only Only contract owner may perform this action
u101 → err-not-token-owner Caller is not the token owner
📦 Contract Functions
Read-Only Functions
Function Description
get-last-token-id → (ok uint) Returns the most recently minted token ID
get-token-uri (token-id uint) → (ok none) Placeholder for metadata URI (currently none)
get-owner (token-id uint) → (ok (optional principal)) Returns the current owner of a token
Public Functions
Function Description
mint (recipient principal) → (ok true) Mints a new NFT to recipient. Only callable by contract owner.
transfer (token-id uint) (sender principal) (recipient principal) Transfers token from sender → recipient. Caller must match sender.
multi-mint (airdrop1 list, airdrop2 list, airdrop3 list, start-last-token-id uint) Batch mints to up to 14,996 addresses across 3 lists. Only callable by contract owner.
🚀 Workflows
1️⃣ Mint a Single NFT
(contract-call? .stacksies mint 'ST123...ABC)

Mints a new token to the given recipient.

Only the contract owner can call this.

2️⃣ Transfer an NFT
(contract-call? .stacksies transfer u1 tx-sender 'ST456...XYZ)

Transfers token u1 from the caller (tx-sender) to another principal.

3️⃣ Batch Airdrop / Multi-Mint
(contract-call? .stacksies multi-mint
(list 'ST123...AAA 'ST123...BBB)
(list 'ST123...CCC)
(list)
u0
)

🔄 STX → sBTC Swap Contract (Stacks / Clarity)
📜 Overview

This smart contract provides a simple interface to swap STX for sBTC using an existing Univ2 liquidity pool deployed on Stacks.

It wraps the swap function of the pool contract and ensures:

The caller has enough STX to cover the swap.

The pool call executes successfully.

Any swap failure reverts with a clear error.

⭐ Features

✅ Swap STX → sBTC in a single call.

✅ Protects against insufficient balances.

✅ Emits the underlying swap event on success.

✅ Safe error codes for debugging.

⚙️ Error Codes
Code Meaning
u100 → ERR-SWAP-FAILED Pool swap call failed
u101 → ERR-INSUFFICIENT-FUNDS Caller balance < requested STX amount
📦 Contract Function
swap-stx-for-sbtc (stx-amount uint)

Swaps the given amount of STX into sBTC using the external pool.

Parameters:

stx-amount → The number of STX tokens to swap.

Flow:

Checks that caller (tx-sender) has enough STX.

Calls the external Univ2 pool contract’s swap function:

Token In: wstx (wrapped STX)

Token Out: sbtc-token

Fee contract: univ2-fees-v1_0_0-0070

If the pool swap fails, aborts with ERR-SWAP-FAILED.

Returns the raw swap event data on success.

Example Call:

(contract-call? .stx-sbtc-swap swap-stx-for-sbtc u1000000) ;; swap 1 STX (1_000_000 microSTX)

🛠️ Usage
Local Deployment (Clarinet)
clarinet new stx-sbtc-swap
cd stx-sbtc-swap

# replace contracts/stx-sbtc-swap.clar with this contract

clarinet check
clarinet console

On Testnet

Deploy via Stacks CLI
or Clarinet.

Open in Hiro Explorer
.

Call swap-stx-for-sbtc with the desired stx-amount.

📄 Security Notes

This contract depends on external Univ2 pool contracts:

Pool: SP20X3DC5R091J8B6YPQT638J8NR1W83KN6TN5BJY.univ2-pool-v1_0_0-0070

Fee: SP20X3DC5R091J8B6YPQT638J8NR1W83KN6TN5BJY.univ2-fees-v1_0_0-0070

Make sure these addresses match the ones on your target chain (testnet/mainnet).

The min-amount-out is hardcoded to u1 (may expose slippage risk).

📄 License

MIT — free to use, fork, and adapt.

Distributes tokens across multiple lists of principals.

Useful for airdrop campaigns or mass NFT launches.

Updates last-token-id after completion.
