---
title: Unexpected Ether Balance
id: SCWE-075
alias: unexpected-ether-balance
platform: []
profiles: [L1]
mappings:
  scsvs-cg: [SCSVS-GOV]
  scsvs-scg: [SCSVS-GOV-3]
  cwe: [665]
status: new
---

## Relationships  
- CWE-665: Improper Initialization  
  [https://cwe.mitre.org/data/definitions/665.html](https://cwe.mitre.org/data/definitions/665.html)  

## Description
When a contract does not properly initialize its state, it may lead to an unexpected Ether balance. This issue arises when a contract either fails to set an initial Ether balance or allows the Ether balance to be manipulated by external contracts. This can lead to errors in contract logic, such as unauthorized withdrawals or incorrect balance tracking.

## Remediation
Ensure that all state variables, especially those related to Ether balances, are properly initialized when the contract is deployed. Use `constructor` functions to set initial balances and carefully track Ether transfers.

### Vulnerable Contract Example
```solidity
contract Example {
    uint public balance;

    // Uninitialized balance leading to unexpected results
    function deposit() public payable {
        balance = balance + msg.value;
    }

    function withdraw(uint _amount) public {
        require(balance >= _amount, "Insufficient funds");
        payable(msg.sender).transfer(_amount);
        balance -= _amount;
    }
}
```
### Fixed Contract Example
```solidity
contract Example {
    uint public balance;

    // Proper initialization of the balance
    constructor() {
        balance = 0;
    }

    function deposit() public payable {
        balance = balance + msg.value;
    }

    function withdraw(uint _amount) public {
        require(balance >= _amount, "Insufficient funds");
        payable(msg.sender).transfer(_amount);
        balance -= _amount;
    }
}
```