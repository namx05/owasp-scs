---
title: Insecure Use of blockhash
id: SCWE-084
alias: insecure-use-of-blockhash
platform: []
profiles: [L1]
mappings:
  scsvs-cg: [SCSVS-CRYPTO]
  scsvs-scg: [SCSVS-CRYPTO-2]
  cwe: [20]
status: new
---

## Relationships  
- CWE-20: Improper Input Validation  
  [https://cwe.mitre.org/data/definitions/20.html](https://cwe.mitre.org/data/definitions/20.html)  

## Description
Using `blockhash` to generate randomness can be insecure as it is publicly available and can be influenced by miners. Relying on blockhash for cryptographic purposes can expose the contract to manipulation by miners or other malicious actors.

## Remediation
Do not rely on `blockhash` for generating randomness. Use more secure and unpredictable sources of randomness, such as using Chainlink VRF or other trusted oracles.

### Vulnerable Contract Example
```solidity
contract Example {
    function getRandomNumber(uint256 _blockNumber) public view returns (uint256) {
        return uint256(blockhash(_blockNumber)); // Using blockhash as a random number
    }
}
```
### Fixed Contract Example
```solidity
contract Example {
    // Use an oracle or VRF for secure random number generation
    function getRandomNumber() public view returns (uint256) {
        // Chainlink VRF or other secure method
    }
}
```