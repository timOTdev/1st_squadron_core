# 2021_09_11_1206_solana_ignition_blastoff_stream

- Tags: #solana #ignition #blastoff #stream #solanahackathon #nft #metaplex

- [NFT / Metaplex Workshop (1:03:50)](https://www.twitch.tv/videos/1144702694)

---

## Notes

- Bartosz Lipinski
- Start with spl.solana.com on tokens, mint.
- Creating a non-fungible token to supply is 1 and decimals to 0.
- Solana-program-libary/token program uses to make a mint.
- Solana-program-libary/token/js/examples.

- **Metaplex docs**
- `Token Metadata` sits on top of the `Token` Program Account.

  - Uses the mint key or mint id and make new account called Metadata.
  - Uses it to generate a new id based off of the unique mint key for your NFT.
  - `MasterEdition` is an admin account that lets you make more limited or open NFTs based off your existing one, can allow other accounts to mint.
  - `seller_fee_basis_points` 10,000 means 100%.
  - On your first sale, all the fees goes to creators accounts in array of public keys.
  - If set to 1000 or 10%, all those futures proceeds split among creator accounts.
  - `primary_sale_happened` bool in MetaData struct lets us know if it's the first sale.
  - Once flipped to true, cannot be flipped back to false.
  - `verified` on Creator struct is a multisig that ensures that the NFT is unique.
  - `update_authority` in MetaData is really ownership of the MetaData. Token and MetaData are separate from each other.
  - You can give someone the Token and they can mint limited NFTs.
  - But the MetaData owner can update the picture and the Token Account can't do anything.
  - The exception is limited, those are clones frozen in time and not affected by any of the new changes from the MetaData owner.
  - A full rights transfer is both the Token and the `update_authority` at the same time.

- js/packages/web/src/actions/nft.tsx
- Walks through minting a master edition, setting up metadata, and sending data to Arweave.

- **URI JSON Schema**
- Left menu "Solana NFT metadata Standard".
- This is the schema of what the meta data shape looks like.
- `image` is the item is what wallets pull from to display.
- `creators` can be spoofed because not verified.

- **Vault**
- Creating fractionalized NFT?
- Token Vault acts as a safe escrow.
- Has fractionlization protocol included with this.
- There are Activated and Combined status and they can mint these tokens.
- Vault limit is currently 256 but can be increased in the future.
- Idea: Dave White Floor Perpetual idea.

- **Auction**
- Modified English Option setup.
- Can be multiple winners.
- Make bids, outbidded, orders are linear, if in range, you win.
- DJ Blau did a drop on origin. Multiple winners, multiple tiers.
- The Metaplex contract is an advance case of the Auction primitive.

- Platforms can ignore the royalty mechanism but it's not moral and Metaplex can't enforce.
- It's a social contract that makes good actors.
- P2P transfers don't have royalty mechanism.

- **Candy Machine**
- nft-candy-machine
- glorified on chain CSV with a pointer
- It counts NFTs minted and move the line on the CSV (has name and uri of NFT).
- If there's no more lines or can't buy it, the CSV do it.
- levicook working with Metaplex Foundation is writing more documentations.
- Anchor has lots of boilerplate but still less than a program.

> 80% Code in rust is "I trust no one, how is this person going to screw me"?

- You can generally just use the Metaplex program and the existing Smart Contracts.
- Governance is the exception where you might need your own smart contract.
- Read this article [Solana SC Pitfalls](https://blog.neodyme.io/posts/solana_common_pitfalls)

- **Q&A**
- Dynamic minting based on upload, look at nft.tsx.
- Minting cost depends Arweave cost.
- Can update metadata after tokens are minted, it's flag that's mutable by default.
- Fair Launch Protocol - program using market dynamics to price NFTs.
- Evolution of candy machine, similar to mango
- Works in differentphases
- 1st is user chooses price in predetermined range.
- 2nd is the median price of all the prices, if median price is fair, you accept or withdraw your deposit.
- 3rd lottery system if there are too many users per nft.

---
