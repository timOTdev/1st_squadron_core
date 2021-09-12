# 2021_09_11_1206_solana_ignition_anchor_intro

- Tags: #solana #ignition #stream #solanahackathon #anchor #introductiontoanchor

- [How to Anchor: An introduction to the Anchor Framework](https://www.youtube.com/watch?v=FmdPAwsqJC4)
- [Serum's Anchor](https://github.com/project-serum/anchor)
- [Cargo Expand](https://github.com/dtolnay/cargo-expand)

---

## Notes

- Chase Barker, Armani Ferrante (founder of anchor), Ryan
- Quick tutorial to Anchor.
- Armani is developer at Alameda research from Apple. Now Serum and Solana.
- Anchor is like Ruby on Rails for Solana.
  - Opinionated framework for developing projects on Solana.
  - It's easier to build on than Solana Native or Rust.
  - Tools for writing smart contracts themselves.
  - Familiar interface.
  - Defines well-defined format for programs to talk to another.
  - Can generate to multiple languages.
  - Big productivity boost and security benefits.
  - What is IDL?
  - Targeted at Solana runtime.
  - Easier to reason about your program with less code.
    > In Solana, there's not a standard way to do things. It's a feature, not a bug.

### Who should it?

- More than 75% developers start with anchor opposed to Rust Native.
- Gotchas with Anchor:
  - Borsch serialization format in Anchor, could or could not be a problem.
  - Stack size instructions. Optimizations needed for codegen.
- Most developers start with Anchor, then would know if they don't need it and eject (easy process).
- First official version to be audited and it will be more secure.
- One known problem needs attention before audit: If you have duplicate mutable accounts, you need to make sure they are unique. It could do unexpected things.

### Anchor demo

- Materials: Project Serum/Anchor on github.
- There are rust docs and typescript docs too.
- There are example directories that you can go through.

- **Example basic_0**
- `#[program]` macro defines your set of instruction handlers.

  - Similar to using it in javascript `await program.rpc.initialize();`
  - There's a 1 to 1 relationship for methods that we can just use the RPC.
  - I think of it like backend code and front end code to call.

- **Example basic_1**
- [Timestamped](https://youtu.be/FmdPAwsqJC4?t=1227)
- `declare_id!` defines your program address and embed it into your program.
  - Important for security reasons.
- `ctx: Context<Initialize>` is default param on all Anchor programs.
  - Defines all the accounts that can be casted into the program.
- `#[derive(Accounts)]` macro is great feature of Anchor that separates your account validation logic from business logic.
  - Easier to reason about because not have to worry about auth.
- `space` is the size of the account.
  - Can set default or bring in u64 in the fn initialize().
- You can fit in as many accounts as the transaction limit allows.
- Tool called _cargo expand_ to expand macro and generate raw low level rust code.
- `#[account(mut)]` marks account as mutable and saves in storage when instructions completes.

- Account is a wrapper that deserializes the raw data underneath and also checks ownership.
  - Necessary because you need for cross-program invocations.
  - That's just how it is with Solana Runtime API.
- `AccountInfo` is unsafe to use unless you validate the Account first.
- Don't use `ProgramAccount` or `CPIAccount`, forget both exists, the new `Account` wrapper replaces both and is better and safer.
- In the javascript, we use `new anchor.BN(1234)` instead of JS's number type to pass for the u64 argument.

- **Example basic_2**
- `anchor test` runs a local validator, test suite provided, and your program.
  - Good for integration test.
  - Can also test with with rust with `cargo test bpf`.
- In Solana, you have to declare all your accounts up front.

  - `#[account(signer)]` checks if the account signed the instructions or abort.
  - `#[account(address = system_program::ID)]` checks if the address is given or abort.
  - System program is needed for the Solana Runtime to initialize an account.

- **Example basic_3**

  - About CPI or calling 1 smart contract from another.
  - puppet_master calls puppet to set some data using `CpiContext`.
  - `SetData` is defiining all the accounts that will be used.
  - CPI = Cross Program Invocation

- **Example basic_4**
- About Token Accounts.
- Allows you to create mint.
- Mint decimals and authority are additional parameters given to account being created.

### Q&A

- PDA - Program Derived Addresses
  - 1st perspective, is an address that is generated deterministicly that can be only used by programs.
  - It creates signatures to use for CPI.
  - 2nd perspective, linked to addresses so they can be used for user's interest.
  - PDA helps to protect from revealing private key?
- Metaplex is the current NFT standard.
- Instruction handlers should validate all the counts.

- IDL generation `anchor parse -h` 2 ways was mentioned.

---
