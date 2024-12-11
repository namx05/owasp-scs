---
title: Code Duplication
id: SCWE-009
alias: code-duplication
platform: []
profiles: [L1]
mappings:
  scsvs-cg: [SCSVS-CODE]
  scsvs-scg: [SCSVS-CODE-1]
  cwe: [1041]
status: new
---

## Relationships
- CWE-1041: Use of Redundant Code
  [https://cwe.mitre.org/data/definitions/1041.html](https://cwe.mitre.org/data/definitions/1041.html)

## Description
Code duplication refers to the use of redundant code, where the same logic or functionality is unnecessarily repeated in different parts of the smart contract. This results in increased code size, reduced maintainability, and higher gas costs for contract deployment and execution. Additionally, redundant code can introduce bugs if the duplicated logic needs to be changed, requiring updates in multiple places.

Smart contracts that exhibit excessive duplication are more prone to errors and inconsistencies, especially when there is a need to modify shared logic. The impact of redundancy grows with the contract's complexity and scale, making maintenance and auditing more challenging.

## Remediation
- **Refactor duplicated code into reusable functions**: Consolidate repeated logic into functions or libraries that can be reused throughout the contract.
- **Adopt modular design**: Use modular design patterns to ensure that functionality is encapsulated in distinct, reusable components.
- **Static analysis tools**: Use automated tools to identify and eliminate redundant code.

## Samples

### Contract with Redundant Code

```solidity
pragma solidity ^0.4.0;

contract CodeDuplication {
    uint public balance;

    function deposit(uint amount) public {
        balance += amount;
    }

    function withdraw(uint amount) public {
        balance -= amount;
    }

    function depositToAnotherAccount(uint amount) public {
        uint balanceOtherAccount = 0;
        balanceOtherAccount += amount; // Redundant code: same logic as deposit
    }
}
```
In this example, the logic for updating the balance is unnecessarily duplicated in multiple functions, leading to redundant code.

### Fixed Code with Refactored Logic
```solidity
pragma solidity ^0.4.0;

contract RefactoredCodeDuplication {
    uint public balance;

    function deposit(uint amount) public {
        _updateBalance(amount);
    }

    function withdraw(uint amount) public {
        _updateBalance(-int(amount));
    }

    function depositToAnotherAccount(uint amount) public {
        uint balanceOtherAccount = 0;
        _updateBalanceForAccount(balanceOtherAccount, amount);
    }

    // Reusable logic to handle balance updates
    function _updateBalance(int amount) internal {
        balance += uint(amount);
    }

    function _updateBalanceForAccount(uint accountBalance, uint amount) internal {
        accountBalance += amount;
    }
}

```

In the improved version, redundant code is eliminated by centralizing the logic into reusable functions (`_updateBalance` and `_updateBalanceForAccount`), making the contract easier to maintain and audit.

