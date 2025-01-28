---
title: Improper Handling of Nonce
id: SCWE-081
alias: improper-handling-of-nonce
platform: []
profiles: [L1]
mappings:
  scsvs-cg: [SCSVS-GOV]
  scsvs-scg: [SCSVS-GOV-2]
  cwe: [20]
status: new
---

## Relationships  
- CWE-20: Improper Input Validation  
  [https://cwe.mitre.org/data/definitions/20.html](https://cwe.mitre.org/data/definitions/20.html)  

## Description
Nonce values are used to ensure that transactions are processed in the correct order and prevent replay attacks. Improper handling or validation of nonces can lead to issues such as transaction replay or improper sequencing of transactions, which can be exploited by attackers.

## Remediation
Always validate nonce values to ensure that they are correctly incremented and avoid reusing nonces. Ensure that nonce handling is robust, especially in cases where external calls are involved, to prevent replay attacks or transaction malleability.

### Vulnerable Contract Example
```solidity
contract Example {
    mapping(address => uint256) public nonces;

    function transfer(address _to, uint256 _amount) public {
        uint256 nonce = nonces[msg.sender]; // Nonce is not validated properly
        nonces[msg.sender] = nonce + 1;     // This could allow replay attacks
        // Transfer logic
    }
}
```
### Fixed Contract Example
```solidity
contract Example {
    mapping(address => uint256) public nonces;

    function transfer(address _to, uint256 _amount, uint256 _nonce) public {
        require(_nonce == nonces[msg.sender], "Invalid nonce");
        nonces[msg.sender] = _nonce + 1;
        // Transfer logic
    }
}
```