---
title: Μετατροπή Smart Contract
description: Μια εξήγηση του γιατί πρέπει να συντάξετε έξυπνα συμβόλαια και τι κάνει στην πραγματικότητα η μεταγλώττιση.
lang: el
incomplete: true
---

Πρέπει να μεταγλωττίσετε το συμβόλαιό σας έτσι ώστε η εφαρμογή ιστού σας και η εικονική μηχανή Ethereum (EVM) να μπορούν να το κατανοήσουν.

## Προαπαιτούμενα {#prerequisites}

Ίσως σας φανεί χρήσιμο να έχετε διαβάσει την εισαγωγή μας στα [έξυπνα συμβόλαια](/developers/docs/smart-contracts/) και στην [εικονική μηχανή Ethereum](/developers/docs/evm/) πριν διαβάσετε σχετικά με τη μεταγλώττιση.

## Η μηχανή EVM {#the-evm}

Για να μπορεί το [EVM](/developers/docs/evm/) να εκτελέσει το συμβόλαιό σας, πρέπει να είναι σε **bytecode**. Η μεταγλώττιση μετατρέπει αυτό:

```solidity
pragma solidity 0.4.24;

contract Greeter {

    function greet() public constant returns (string) {
        return "Hello";
    }

}
```

**σε αυτό**

```
PUSH1 0x80 PUSH1 0x40 MSTORE PUSH1 0x4 CALLDATASIZE LT PUSH2 0x41 JUMPI PUSH1 0x0 CALLDATALOAD PUSH29 0x100000000000000000000000000000000000000000000000000000000 SWAP1 DIV PUSH4 0xFFFFFFFF AND DUP1 PUSH4 0xCFAE3217 EQ PUSH2 0x46 JUMPI JUMPDEST PUSH1 0x0 DUP1 REVERT JUMPDEST CALLVALUE DUP1 ISZERO PUSH2 0x52 JUMPI PUSH1 0x0 DUP1 REVERT JUMPDEST POP PUSH2 0x5B PUSH2 0xD6 JUMP JUMPDEST PUSH1 0x40 MLOAD DUP1 DUP1 PUSH1 0x20 ADD DUP3 DUP2 SUB DUP3 MSTORE DUP4 DUP2 DUP2 MLOAD DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP DUP1 MLOAD SWAP1 PUSH1 0x20 ADD SWAP1 DUP1 DUP4 DUP4 PUSH1 0x0 JUMPDEST DUP4 DUP2 LT ISZERO PUSH2 0x9B JUMPI DUP1 DUP3 ADD MLOAD DUP2 DUP5 ADD MSTORE PUSH1 0x20 DUP2 ADD SWAP1 POP PUSH2 0x80 JUMP JUMPDEST POP POP POP POP SWAP1 POP SWAP1 DUP2 ADD SWAP1 PUSH1 0x1F AND DUP1 ISZERO PUSH2 0xC8 JUMPI DUP1 DUP3 SUB DUP1 MLOAD PUSH1 0x1 DUP4 PUSH1 0x20 SUB PUSH2 0x100 EXP SUB NOT AND DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP JUMPDEST POP SWAP3 POP POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 RETURN JUMPDEST PUSH1 0x60 PUSH1 0x40 DUP1 MLOAD SWAP1 DUP2 ADD PUSH1 0x40 MSTORE DUP1 PUSH1 0x5 DUP2 MSTORE PUSH1 0x20 ADD PUSH32 0x48656C6C6F000000000000000000000000000000000000000000000000000000 DUP2 MSTORE POP SWAP1 POP SWAP1 JUMP STOP LOG1 PUSH6 0x627A7A723058 KECCAK256 SLT 0xec 0xe 0xf5 0xf8 SLT 0xc7 0x2d STATICCALL ADDRESS SHR 0xdb COINBASE 0xb1 BALANCE 0xe8 0xf8 DUP14 0xda 0xad DUP13 LOG1 0x4c 0xb4 0x26 0xc2 DELEGATECALL PUSH7 0x8994D3E002900
```

Αυτά ονομάζονται **opcodes**. Τα opcodes EVM είναι οι οδηγίες χαμηλού επιπέδου που μπορεί να εκτελέσει η Εικονική Μηχανή Ethereum (EVM). Κάθε opcode αντιπροσωπεύει μια συγκεκριμένη λειτουργία, όπως αριθμητικές πράξεις, λογικές πράξεις, χειρισμό δεδομένων, ροή ελέγχου κ. λπ.

[Περισσότερα για τα opcodes](/developers/docs/evm/opcodes/)

## Εφαρμογές ιστού {#web-applications}

Ο μεταγλωττιστής θα παράγει επίσης τη **Application Binary Interface (ABI)** την οποία χρειάζεστε για να κατανοήσει η εφαρμογή σας το συμβόλαιο και να καλέσει τις λειτουργίες του συμβολαίου.

Το ABI είναι ένα αρχείο JSON που περιγράφει το αναπτυγμένο συμβόλαιο και τις λειτουργίες του έξυπνου συμβολαίου του. Αυτό βοηθά στη γεφύρωση του χάσματος μεταξύ web2 και web3

Μια [βιβλιοθήκη πελάτη JavaScript](/developers/docs/apis/javascript/) θα διαβάσει το **ABI** για να μπορέσετε να καλέσετε το έξυπνο συμβόλαιό σας στη διεπαφή της εφαρμογής ιστού σας.

Παρακάτω είναι το ABI για το συμβόλαιο του ERC-20 token. Ένα ERC-20 είναι ένα token που μπορείτε να ανταλλάξετε στο Ethereum.

```json
[
  {
    "constant": true,
    "inputs": [],
    "name": "name",
    "outputs": [
      {
        "name": "",
        "type": "string"
      }
    ],
    "payable": false,
    "stateMutability": "view",
    "type": "function"
  },
  {
    "constant": false,
    "inputs": [
      {
        "name": "_spender",
        "type": "address"
      },
      {
        "name": "_value",
        "type": "uint256"
      }
    ],
    "name": "approve",
    "outputs": [
      {
        "name": "",
        "type": "bool"
      }
    ],
    "payable": false,
    "stateMutability": "nonpayable",
    "type": "function"
  },
  {
    "constant": true,
    "inputs": [],
    "name": "totalSupply",
    "outputs": [
      {
        "name": "",
        "type": "uint256"
      }
    ],
    "payable": false,
    "stateMutability": "view",
    "type": "function"
  },
  {
    "constant": false,
    "inputs": [
      {
        "name": "_from",
        "type": "address"
      },
      {
        "name": "_to",
        "type": "address"
      },
      {
        "name": "_value",
        "type": "uint256"
      }
    ],
    "name": "transferFrom",
    "outputs": [
      {
        "name": "",
        "type": "bool"
      }
    ],
    "payable": false,
    "stateMutability": "nonpayable",
    "type": "function"
  },
  {
    "constant": true,
    "inputs": [],
    "name": "decimals",
    "outputs": [
      {
        "name": "",
        "type": "uint8"
      }
    ],
    "payable": false,
    "stateMutability": "view",
    "type": "function"
  },
  {
    "constant": true,
    "inputs": [
      {
        "name": "_owner",
        "type": "address"
      }
    ],
    "name": "balanceOf",
    "outputs": [
      {
        "name": "balance",
        "type": "uint256"
      }
    ],
    "payable": false,
    "stateMutability": "view",
    "type": "function"
  },
  {
    "constant": true,
    "inputs": [],
    "name": "symbol",
    "outputs": [
      {
        "name": "",
        "type": "string"
      }
    ],
    "payable": false,
    "stateMutability": "view",
    "type": "function"
  },
  {
    "constant": false,
    "inputs": [
      {
        "name": "_to",
        "type": "address"
      },
      {
        "name": "_value",
        "type": "uint256"
      }
    ],
    "name": "transfer",
    "outputs": [
      {
        "name": "",
        "type": "bool"
      }
    ],
    "payable": false,
    "stateMutability": "nonpayable",
    "type": "function"
  },
  {
    "constant": true,
    "inputs": [
      {
        "name": "_owner",
        "type": "address"
      },
      {
        "name": "_spender",
        "type": "address"
      }
    ],
    "name": "allowance",
    "outputs": [
      {
        "name": "",
        "type": "uint256"
      }
    ],
    "payable": false,
    "stateMutability": "view",
    "type": "function"
  },
  {
    "payable": true,
    "stateMutability": "payable",
    "type": "fallback"
  },
  {
    "anonymous": false,
    "inputs": [
      {
        "indexed": true,
        "name": "owner",
        "type": "address"
      },
      {
        "indexed": true,
        "name": "spender",
        "type": "address"
      },
      {
        "indexed": false,
        "name": "value",
        "type": "uint256"
      }
    ],
    "name": "Approval",
    "type": "event"
  },
  {
    "anonymous": false,
    "inputs": [
      {
        "indexed": true,
        "name": "from",
        "type": "address"
      },
      {
        "indexed": true,
        "name": "to",
        "type": "address"
      },
      {
        "indexed": false,
        "name": "value",
        "type": "uint256"
      }
    ],
    "name": "Transfer",
    "type": "event"
  }
]
```

## Περισσότερες πληροφορίες {#further-reading}

- [ABI spec](https://solidity.readthedocs.io/en/v0.7.0/abi-spec.html) _– Solidity_

## Σχετικά θέματα {#related-topics}

- [Βιβλιοθήκες πελάτη Javascript](/developers/docs/apis/javascript/)
- [Εικονική μηχανή Ethereum](/developers/docs/evm/)
