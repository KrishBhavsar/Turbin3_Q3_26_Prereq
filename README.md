# Pre-Req Vault

An Anchor-based SOL vault built for the Turbin Builders prerequisite challenge. A user can initialize a vault, deposit SOL, withdraw SOL, and close the vault.

## Program details

- **Network:** Solana Devnet
- **Program public address:** [`5zBZNgsuR6BHH73nmdP6mozacSKXowpX5me5q59jhFvM`](https://explorer.solana.com/address/5zBZNgsuR6BHH73nmdP6mozacSKXowpX5me5q59jhFvM?cluster=devnet)

## Task 2: withdrawal registration

My Task 2 change is in [`withdraw.rs`](programs/pre-req-vault/src/instructions/withdraw.rs). After the vault transfers SOL back to the user, the `withdraw` instruction makes a Cross-Program Invocation (CPI) to Turbin's prerequisite registration program.

The withdrawal flow is:

1. The vault PDA signs and transfers the requested SOL amount to the user.
2. The program derives and validates the user's `prereqs` PDA for Turbin's registration program.
3. A CPI calls the registration program's `initialize` instruction with my GitHub username, `KrishBhavsar`.

This records the completed withdrawal as part of the same transaction. If the CPI fails, the complete transaction is reverted, including the SOL transfer.

## Architecture

```text
User
  | signs withdrawal
  v
Pre-Req Vault Program
  |-- vault PDA signs --> transfers SOL to the user
  '-- CPI --> Turbin Prerequisite Program --> creates/updates the user's prereqs PDA
```

## Run locally

```bash
anchor build
anchor test
```

## Submission resources

- [YouTube explanation](https://youtu.be/Fq8NwG50D3U)
- [Architecture diagram](https://drive.google.com/file/d/1UWIyiFP_vrRIFUvb6H-3I1E1kvThrF4O/view?usp=sharing)
