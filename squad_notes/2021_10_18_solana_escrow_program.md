# 2021_10_18_solana_escrow_program

- Tags: #icarusnode #solana #escrowprogram #paulx

- [Article Link](https://paulx.dev/blog/2021/01/14/programming-on-solana-an-introduction/)
- [Paul's Twitter](https://twitter.com/paulxpaulxpaulx)
- [Final Code](https://github.com/paul-schaaf/solana-escrow)
- [Template Repo](https://github.com/mvines/solana-bpf-program-template)

- Template vs Forking?

```txt
A new fork includes the entire commit history of the parent repository, while a repository created from a template starts with a single commit.

Commits to a fork don't appear in your contributions graph, while commits to a repository created from a template do appear in your contribution graph.

A fork can be a temporary way to contribute code to an existing project, while creating a repository from a template starts a new project quickly.

SRC: https://stackoverflow.com/questions/62082123/github-what-is-the-difference-between-template-and-fork-concepts-and-when-to-us
SRC: https://docs.github.com/en/enterprise-server@2.22/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template
```

---

## notes

- Escrow program is about trustless 3rd party governed by code (smart contract, aka program).
- _entrypoints_ are where all calls pass through.

- A program is processed by _BPF Loader_, which is a program itself.
- _BPF Loader_ takes `program_id`, `instruction_data`, and `accounts`.

- Solana program are stateless.
- Data is stored and persisted with an _Account_.
- Each account has an _owner_, having the power to withdraw from account and change data.
- However, anyone can deposit into the account.

- Programs can be owners for other programs. Confused yet? :)
- Often, the `System Program` is set as the owner of the account.
- This is because basic SOL transactions are usually handled by the `system program`.

- The _NativeLoader_ owns the _BPF Loader_ and the _System Program_.
- Nativeloader has special privileges.

- Each account holds _data_ and SOL.
- Programs are also stored inside accounts and marked `executable`.

- Important: All accounts to be interacted with needs to pass through the `entrypoint` function.
- This lets it control the flow and avoid any collisions of things like double-writing the same file.
- If condition is violated, all transactions fail.

### Code Structure

- Not sure if this structure is article-specific or boilerplate.
- My own intepretation:

```text
entrypoint => processor => instruction => state
error wraps around whole process?

├─ src
│  ├─ lib.rs -> where you bring in modules, think npm packages?
│  ├─ entrypoint.rs -> where all data and arguments pass through
│  ├─ processor.rs -> arguments sent to processor to be handled, has the logic
│  ├─ instruction.rs -> instructions helps translate processor' received arguments, (de)serialize data
│  ├─ state.rs -> process can choose to write data to state, (de)serialize state
│  ├─ error.rs -> hold errors
├─ .gitignore
├─ Cargo.lock
├─ Cargo.toml
├─ Xargo.toml
```

### Token Program

- Check out the article to see the diagram, won't include here.
- Basically the token program creates 4 additional accounts for the tokens.
- Alice's X account, Alice's Y account, Bob's X account, Bob's Y account.

- It's not practical for Alice to have a private key for these additional accounts.
- Instead, the token program assigns the `owner` attribute to Alice main account address instead.
- These will be the main addresses from Alice's and Bob's main account.
  - IE Public Key of Alice `HRf39cNRWmNBqngenA1i1pzTW47uqxPzvYvtHX81chuj` set as token account owner
- The private keys for the token accounts don't really matter because only the `owner` attribute matters.

- The token account owner attribute is NOT the same as the account owner.

- A. The token account owner (AKA User-space information)

  - Attribute stored inside token account `data` and has the following:
  - Fields: `mint`, `owner`, `amount`, `delegate`, `state`, `is_native`, `delegated_amount`, `close_authority`
  - `mint` is a field that has metadata for the official token, like SOL, to make sure it holds the right asset for exchange.
  - [Source](https://github.com/solana-labs/solana-program-library/blob/80e29ef6b9a081d457849a2ca42db50d7da0e37e/token/program/src/state.rs#L86)

- B. The program account owner

  - Stored on internal Solana attribute
  - Will always be a program
  - This is stored on the fields of the AccountInfo struct
  - Fields: `key`, `is_signer`, `is_writable`, `lamports`, `data`, `owner`, `executable`, `rent_epoch`
  - [Source](https://docs.rs/solana-program/1.5.0/solana_program/account_info/struct.AccountInfo.html#fields)

> To re-emphasize, the token account stores related information inside its "data" field, aka user space information. The main account information is stored on the fields of the Account, not in the "data" field..

## Transferring Ownership

- So Alice has X account.
- The `mint` tells that the token is of X type, like SOL. So she can't put SRM or RAY tokens in.
- The `owner` attribute on the token account is her main wallet's address.
- Now to transfer, she uses a function that changes the `owner` from her address to the _escrow program address_.
- This _escrow program address_ is also known as the _Program Derived Address_.

---
