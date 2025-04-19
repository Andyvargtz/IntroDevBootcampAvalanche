---
icon: square-small
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# What is the EVM?

The EVM (Ethereum Virtual Machine) is a virtual machine that executes smart contracts on the Ethereum network. It is the core component that enables the execution of decentralized code on the Ethereum blockchain.

## Main Features

- **Turing-complete**: Can execute any program that can be expressed in code
- **Isolation**: Smart contracts run in an isolated environment
- **Deterministic**: Same input always produces the same output
- **Gas**: Fee system to prevent spam and abuse

## Architecture

The EVM operates as a state machine that processes transactions and updates the blockchain state. Each node in the Ethereum network runs a copy of the EVM to maintain state consistency.

## Programming Languages

Smart contracts on the EVM can be written in several languages:
- Solidity (most popular)
- Vyper
- Yul (intermediate language)
- LLL (Low-Level Lisp-like Language)

## Importance

The EVM has been fundamental for:
1. Enabling decentralized applications (dApps)
2. Creating tokens and standards like ERC-20 and ERC-721
3. Allowing interoperability between different projects
4. Serving as a base for other EVM-compatible blockchains
