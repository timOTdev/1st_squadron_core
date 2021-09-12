# 2021_09_12_1000_solana_ignition_mango

- Tags: #solana #ignition #blastoff #stream #solanahackathon #mangomarket

- [Mango Workshop](https://www.youtube.com/watch?v=acZiCt5pSJI)

---

## Notes

- Dafydd Durairaj, Maximilian Schneider

- Max is a core contributor.
- Mango doc presented but no substitute to the code.
- TODO: Get link for doc.
- Covering intermediate level of programming and more on program side than client.

- 6 Types of important accounts.
- **MangoGroup**
  - Holds all the information so basically like a cache account.
  - Rarely written to, usually read-only.
- **MangoAccount**
  - Account for the user.
- **MangoCache**
  - Solana Txs limited to 1200 bytes of data.
  - PubKey is already 32bytes.
  - Roughly 30 accounts pass in.
  - Helps pull important information to bypass this limitation.
  - Usually passed as read-only. If passed as write, makes whole app single threaded.
  - Only 1 account can interact with a transaction at a time.
- **RootBank**
  - Another mechanism to keep things multi-thread.
  - Only 1 RootBank per token.
- **NodeBank**
  - USDC can have up to 8 nodebanks.
  - That way you can interact with different cores and not have blocking interactions.
- **EventQueue**
  - Slightly modified version of Serum Dex's event queue.
- **Keeper**

  - Look at client mango v3.
  - Keep track of funding.

- Skipped out on rest of demo.

### Code demo

- Advanced Order Types

1. Allow user to create an Advanced Orders account and store the pubkey in his MangoAccount.
2. Allow user to add Advanced Order to Advanced Orders account.
3. Another instruction to let anyone trigger the Advanced Orders on the account.

- Give initiator an incentive to keep track of these accounts amd trigger them.

---
