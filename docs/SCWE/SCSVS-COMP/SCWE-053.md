---
title: Weak Sources of Randomness from Chain Attributes
id: SCWE-053
alias: weak-randomness-chain-attributes
platform: []
profiles: [L1]
mappings:
  scsvs-cg: []
  scsvs-scg: []
  cwe: [336]
status: new
---

## Relationships  
- CWE-336: Predictable Random Number Generator  
  [https://cwe.mitre.org/data/definitions/336.html](https://cwe.mitre.org/data/definitions/336.html)  

## Description
Using weak or predictable sources of randomness in smart contracts, such as block timestamps or block numbers, can lead to vulnerabilities. These sources can be manipulated by miners or attackers, resulting in predictable outcomes and a lack of true randomness. This is particularly risky for applications involving lotteries, games, or any contract that relies on secure random number generation.

## Remediation
To mitigate this issue, avoid using chain attributes like block numbers, block timestamps, or gas limits as sources of randomness. Instead, use secure randomness sources, such as the `oracle` services or more advanced methods like Chainlink VRF (Verifiable Random Function), which provide cryptographically secure randomness.

### Vulnerable Contract Example
```solidity
contract RandomnessExample {
    function getRandomNumber() public view returns (uint) {
        return uint(keccak256(abi.encodePacked(block.timestamp, block.difficulty))); // Weak randomness
    }
}
```
### Fixed Contract Example
```solidity
contract SecureRandomnessExample {
    address private oracle;  // Example using an oracle for secure randomness
    
    constructor(address _oracle) {
        oracle = _oracle;
    }
    
    function getRandomNumber() public view returns (uint) {
        // Replace with an oracle service that provides secure randomness, e.g., Chainlink VRF
        return uint(keccak256(abi.encodePacked(oracle)));  // Placeholder for secure randomness
    }
}
```