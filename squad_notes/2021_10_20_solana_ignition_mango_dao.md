# 2021_10_20_solana_ignition_mango_dao

- Tags: #icarusnode #magomarket #dao #ignition #twitch

- [Mango DAO Demo (1:12:18)](https://www.twitch.tv/videos/1175529445)
- [Solana Governance Demo Doc](https://marred-ragamuffin-111.notion.site/Solana-Governance-Demo-e188492717644a6e8288a7d8379263e8)

---

## notes

- Maximilian Schneider
- How to work with governance and DAO

- All this works on devnet, can test it out there.
- [Vanilla governance program](https://solana-labs.github.io/oyster-gov/#/)

- _Council Mint_ for multisig that few people have control.
- _Community Mint_ for governance tokens.

- Token holders control resources like treasury, programs, and other things
- _Realms_ is the highest level of governance and connected to community token.
- Each realm can have many _governances_.
- _Governance_ is an authority and handles various operations like voting, validation, etc.
  - In reality, it is just a wallet that is influence by the mango token.
  - It just is the "authority" because it handles incoming tokens. Like a voting manager who tallies up all the votes (tokens in this case).
  - The Governance is also the owner of the token account.
  - This is so it can delegate and

### Factors

- Every proposal is just basically code that gets executed.
- `mint address` is mint authority or person who minted
- `min tokens to create proposal`
- `min instruction hold up time (days)` is days until code is executed??
- `max voting time (days)`
- `yes vote threshold (%)` - how many users need to vote yes to pass the proposal, like a "quorum"

### Proposals

- Make a github gist for proposal.
- Add link to gist when making proposal.

- Later it simulates transaction on the validator.
- Then you can verify on the Solana explorer later.
- If it fails, there's either a bug or too complicated of a scenario.

- Tokens are locked until the voting process is completed.
- Don't forget to release your tokens after the voting process is over.
- If you withdraw tokens early, your vote gets cancelled.
- There is a limit on how mnay proposals can be voted on at a time.

### Handling Exploits

- Council can take over to best handle situation.
- You don't want public to know because they can hack the fix if announced.

### Future proposals

- Voter Weights add-in
- Vested tokens
- Hidden voting
- Treasury management

## Questions

- Realm > Governance > Proposal model is standard?
- How to make complete anonymity?
- Best protocols/projects to learn simple DAO?
  - Oyster, Mango

---
