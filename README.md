# ViriumDAO Smart Contract Documentation

First token deployment in Goerli: https://goerli.etherscan.io/address/0x989f3c571837ae36866df22af9c735b9d8ef5a98#code

## Overview

The `ViriumDAO` smart contract is an implementation of an ERC-20 token with additional features allowing for burning, pausing, and ownership control, among others. It's built using the Solidity programming language version 0.8.20 and extends functionality from the OpenZeppelin contracts library.

## Features

### ERC20 Standard
- The contract follows the ERC20 token standard, providing basic functionalities such as transferring, balance querying, and allowance setting.

### Burnable
- Tokens can be destroyed by their owners, reducing the total supply.

### Pausable
- The contract owner can pause or unpause token transfers, which could be a necessary action in case of an emergency.

### Ownable
- Some functions are restricted to be callable only by the contract's owner.

### Permit
- The contract supports gasless approvals through the ERC-20 Permit extension, allowing holders to give spending allowances to others via a signed message.

### Votes
- The contract incorporates the ERC20Votes extension, which facilitates on-chain voting.

## Contract Details

### Constructor

```solidity
constructor(address initialOwner)
    ERC20("ViriumDAO", "VDAO")
    Ownable(initialOwner)
    ERC20Permit("ViriumDAO")
{
    _mint(msg.sender, 1000000000 * 10 ** decimals());
}
```
- Initializes the contract with the name "ViriumDAO" and symbol "VDAO".
- Sets the `initialOwner` as the owner of the contract.
- Mints 1 billion tokens to the address deploying the contract.

### Pause and Unpause Functions

```solidity
function pause() public onlyOwner {
    _pause();
}

function unpause() public onlyOwner {
    _unpause();
}
```
- These functions allow the contract owner to pause or unpause token transfers.

### Override Functions

```solidity
function _update(address from, address to, uint256 value)
    internal
    override(ERC20, ERC20Pausable, ERC20Votes)
{
    super._update(from, to, value);
}

function nonces(address owner)
    public
    view
    override(ERC20Permit, Nonces)
    returns (uint256)
{
    return super.nonces(owner);
}
```
- These functions are overrides required by Solidity for the contract to function correctly with the integrated OpenZeppelin extensions.

### Security Contact

- For security concerns, contact `contact@virium.org`.

## Important

This documentation is a simplified guide and does not cover all technical details. It's crucial to have a solid understanding of Solidity, the Ethereum blockchain, and the OpenZeppelin library when interacting with this contract.
