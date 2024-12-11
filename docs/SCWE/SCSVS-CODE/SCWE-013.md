---
title: Dead Code
id: SCWE-013
alias: dead-code
platform: []
profiles: [L1]
mappings:
  scsvs-cg: [SCSVS-CODE]
  scsvs-scg: [SCSVS-CODE-2]
  cwe: [561]
status: new
---

## Relationships
- **CWE-561: Dead Code**  
  [CWE-561](https://cwe.mitre.org/data/definitions/561.html)  
  Description: Dead code refers to sections of code that are written but never executed or used. It does not contribute to the program's logic and can increase contract complexity, introduce bugs, and waste computational resources.

## Description
Dead code refers to any part of a smart contract that is written but never executed during the contract's lifecycle. This can happen for several reasons, including leftover code from previous implementations or logic that is no longer needed. Dead code unnecessarily increases contract size, making it harder to audit, maintain, and increases the gas cost for contract deployment and execution.

### Key issues:
- **Increased contract size**: Larger contracts lead to higher deployment costs.
- **Reduced clarity and maintainability**: Unnecessary code can confuse developers and lead to mistakes in future code changes.
- **Higher attack surface**: Although dead code doesn't run, it could still be misused by attackers in case the contract's logic is altered.

## Remediation
- **Remove unused code**: Periodically clean up the codebase to ensure only necessary functions and variables remain.
- **Refactor contract logic**: Keep the contract logic simple and modular. If a piece of code is no longer needed, remove it completely.
- **Regular audits and code reviews**: Set up regular code reviews to identify and eliminate dead code as part of the contract development lifecycle.

## Samples

### Example of Dead Code

```solidity
pragma solidity ^0.4.0;

contract DeadCodeExample {
    uint public balance;

    // This function allows users to deposit funds
    function deposit(uint amount) public {
        balance += amount;
    }

    // This function is never used and adds unnecessary complexity to the contract
    function unusedWithdrawal() public {
        // Logic that is never called
        balance -= 10;
    }
}

contract Test {
    DeadCodeExample example;

    constructor() public {
        example = new DeadCodeExample();
    }

    // Calling the deposit function from the DeadCodeExample contract
    function testDeposit() public {
        example.deposit(100);  // Calling the deposit function on the example contract
    }
}
```
In this example, the function `unusedWithdrawal()` in the `DeadCodeExample` contract is never called or used in the code. It adds unnecessary complexity, increases contract size, and wastes computational resources.

### Optimized Contract Without Dead Code
```solidity
pragma solidity ^0.4.0;

contract DeadCodeExample {
    uint public balance;

    // This function allows users to deposit funds
    function deposit(uint amount) public {
        balance += amount;
    }
}

contract Test {
    DeadCodeExample example;

    constructor() public {
        example = new DeadCodeExample();
    }

    // Calling the deposit function from the DeadCodeExample contract
    function testDeposit() public {
        example.deposit(100);  // Calling the deposit function on the example contract
    }
}
```
In the optimized version, the `unusedWithdrawal()` function has been removed from the `DeadCodeExample` contract, reducing the size and complexity of the code and making it easier to maintain and audit.