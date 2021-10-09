# 2021_09_23_2034_gentle_intro_solana

- Tags: #icarusnode

- [Link](https://kirima.vercel.app/post/gentleintrosolana)
- ***

## notes

- Use Ubuntu program on windows instead of WSL program.
  - Can download from Windows app store.
  - I downloaded Ubuntu 20.04 LTS.

### Account recovery Error

```txt
// Error
==================================================================================
Recover the intermediate account's ephemeral keypair file with
`solana-keygen recover` and the following 12-word seed phrase:
==================================================================================
gentle sadness dune agree monitor unusual pelican family nuclear surge game picnic
==================================================================================
To resume a deploy, pass the recovered keypair as
the [PROGRAM_ADDRESS_SIGNER] argument to `solana deploy` or
as the [BUFFER_SIGNER] to `solana program deploy` or `solana write-buffer'.
Or to recover the account's lamports, pass it as the
[BUFFER_ACCOUNT_ADDRESS] argument to `solana program close`.
==================================================================================
```

- Run `solana-keygen recover --force`.
- It will prompt for your 12 word seed phrase from when you created the first time.
- The pub key that returns is your public key.

```
// Resolution

[recover] seed phrase:
[recover] If this seed phrase has an associated passphrase, enter it now. Otherwise, press ENTER to continue:
Recovered pubkey `HytrkWSRvaQm7qeV5ycAVcFnN8SRSt5cAdoMJMfgWEmJ`. Continue? (y/n): y
```

### Insufficient funds for spend error

```txt
// Error
Error: Account HytrkWSRvaQm7qeV5ycAVcFnN8SRSt5cAdoMJMfgWEmJ has insufficient funds for spend (0.42437208 SOL) + fee (0.000325 SOL)
```

- Depends on what cluster your on.
- If you're on localhost, see [article](https://docs.solana.com/cli/usage).
  - Run `solana airdrop 1` to get 1 SOL for your wallet.
  - Run `solana balance` to check how much you have.
- If you're on devnet, see [article](https://docs.solana.com/cli/transfer-tokens).
  - This command is different.
  - Run `solana airdrop 1 [YOUR PUBLIC KEY] --url https://api.devnet.solana.com`

```txt
// Output
Requesting airdrop of 1 SOL

Signature: 5Jefbi6ZDuokvYqScYVZxx167bYXz13tApPwHXPYLYGtwaLUy4qt8qstC3oJycDpsFTr33qn3t6AaQY2D5FTty4e

1 SOL
```

---

## navigation

- [index](../index) > [icarus](node) > [2021_09_23_2034_gentle_intro_solana](2021_09_23_2034_gentle_intro_solana)

---
