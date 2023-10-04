# ENS audit details
- Total Prize Pool: $24,500 USDC 
  - HM awards: $16,500 USDC 
  - Analysis awards: $1,000 USDC 
  - QA awards: $500 USDC 
  - Bot Race awards: $1,500 USDC 
  - Gas awards: $500 USDC
  - Judge awards: $2,400 USDC 
  - Lookout awards: $1,600 USDC 
  - Scout awards: $500 USDC 
- Join [C4 Discord](https://discord.gg/code4rena) to register
- Submit findings [using the C4 form](https://code4rena.com/contests/2023-10-ens/submit)
- [Read our guidelines for more details](https://docs.code4rena.com/roles/wardens)
- Starts October 5, 2023 20:00 UTC 
- Ends October 11, 2023 20:00 UTC

# Overview

## About ENS

ENS is a decentralised naming service built on top of Ethereum, and designed to resolve a wide array of resources including blockchain addresses, decentralised content, and user profile information.

Developer documentation can be found [here](https://docs.ens.domains/).

Information on existing ENS deployments can be found [here](https://docs.ens.domains/ens-deployments).


## Links

- **Previous audits:** n/a
- **Documentation:** https://docs.ens.domains
- **Website:** https://ens.domains
- **Twitter:** https://twitter.com/ensdomains
- **Discord:** https://chat.ens.domains


# Scope

| Contract | SLOC | Purpose | Libraries used |  
| ----------- | ----------- | ----------- | ----------- |
| [contracts/ERC20MultiDelegate.sol](https://github.com/code-423n4/2023-10-ens/blob/main/contracts/ERC20MultiDelegate.sol) | 216 | ERC20Votes compatible multi-delegation contract to manage user votings | [`@openzeppelin/*`](https://openzeppelin.com/contracts/) |

## Out of scope

All files not listed above

# Additional Context

The contract implements a multi-delegation mechanism for ERC20 tokens that support the ERC20Votes extension. This allows users to delegate their voting power to multiple addresses in a single transaction.

The contract relies on OpenZeppelin's libraries for standard ERC20 and ERC1155 functionalities. It utilizes Solidity's native features for creating proxy contracts, thereby enabling unique delegation capabilities for each user-delegate pair.

The contract does not use any custom cryptographic algorithms, but it employs the ERC20Votes and ERC1155 standards to manage delegation and token metadata, respectively.

## Attack Ideas (Where to look for bugs)

  - Check for proper permissions and roles.
  - Ensure that the delegateMulti function handles array inputs correctly.
  - Validate the logic for transferring between proxy delegators.

## Main Invariants

  - Tokens should only be transferred between approved delegators.
  - The owner should only have the ability to change the URI for ERC1155 metadata.

## Scoping Details 

```
- If you have a public code repo, please share it here: https://github.com/ensdomains/governance 
How many contracts are in scope?: 1
Total SLoC for these contracts?: 216
How many external imports are there?: 5
How many separate interfaces and struct definitions are there for the contracts within scope?: 0
Does most of your code generally use composition or inheritance?: Inheritance
How many external calls?: Multiple, primarily for ERC20 and ERC1155 functions
Overall line coverage percentage provided by your tests?: Stmts: 100%, Branch: 91.67%, Funcs: 100%, Lines 100%
Is this an upgrade of an existing system?: No
Check all that apply (e.g., timelock, NFT, AMM, ERC20, rollups, etc.): ERC20, ERC1155
Is there a need to understand a separate part of the codebase/get context in order to audit this part of the protocol?: No
Describe required context: N/A
Does it use an oracle?: No
Describe any novel or unique curve logic or mathematical models your code uses: N/A
Is this either a fork of or an alternate implementation of another project?: No
Does it use a side-chain?: No
Describe any specific areas you would like addressed: Multi-delegation logic, proxy delegators
```

# Tests

```bash
# install npm packages (if you haven't already)
yarn
# run in first terminal
npx hardhat node
# run in another terminal
yarn test test/delegatemulti.js
# for coverage
yarn coverage
```
