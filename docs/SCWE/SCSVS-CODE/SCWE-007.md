---
title: Unmaintainable Code Structure
id: SCWE-007
alias: unmaintainable-code-structure
platform: []
profiles: [L1]
mappings:
  scsvs-cg: [SCSVS-CODE]
  scsvs-scg: [SCSVS-CODE-2]
  cwe: [1104]
status: new
---

## Relationships
- CWE-1104: Use of Unmaintained Third Party Components
  [https://cwe.mitre.org/data/definitions/1104.html](https://cwe.mitre.org/data/definitions/1104.html)

## Description
Unmaintainable code structure refers to a situation where a contract's code is poorly organized, difficult to read, or hard to modify. This may occur due to poor naming conventions, excessive complexity, lack of modularization, and insufficient comments or documentation. It makes it difficult for developers to make changes, fix bugs, or extend functionality without introducing new errors.

Some common problems include:
- Excessive length of functions or contracts.
- Lack of clear separation between different functionalities.
- Redundant or poorly organized code leading to a high risk of introducing bugs during maintenance.
- Inconsistent naming conventions and lack of documentation.

Unmaintainable code structures increase the likelihood of introducing vulnerabilities, and they reduce the overall development efficiency, leading to costly mistakes.

## Remediation
- **Modularize the Code:** Break down large contracts or functions into smaller, more manageable pieces. This improves readability and maintainability.
- **Follow Coding Standards:** Adhere to established coding standards and best practices to ensure consistent naming, formatting, and structure.
- **Document the Code:** Provide detailed comments and documentation for complex sections of the code.
- **Refactor Periodically:** Regularly refactor code to improve its structure, remove redundancy, and enhance readability.

## Samples

### Vulnerable Contract with Unmaintainable Code

```solidity
pragma solidity ^0.4.0;

contract Unmaintainable {
    uint public balance;

    function deposit(uint amount) public {
        // Complex code here, no documentation, hard to maintain
        balance += amount;
        uint temp = amount;
        uint result = temp + 1;
        temp = temp - 2;
        // More redundant or complex logic
    }

    function withdraw(uint amount) public {
        // Complex code here, no documentation, hard to maintain
        balance -= amount;
        uint temp = amount;
        uint result = temp * 2;
        temp = temp / 3;
        // More redundant or complex logic
    }
}
```

In the above example, both `deposit` and `withdraw` functions have redundant logic, and the lack of documentation makes it hard to maintain or modify the contract. Additionally, the functions are unnecessarily complex, making future changes prone to errors.

### Improved Code Structure with Modularization
```solidity
pragma solidity ^0.4.0;

contract Deposit {
    uint public balance;

    function deposit(uint amount) public {
        balance += amount;
    }
}

contract Withdraw {
    uint public balance;

    function withdraw(uint amount) public {
        balance -= amount;
    }
}

contract Bank is Deposit, Withdraw {
    // Clear separation between Deposit and Withdraw functionality
    // Each contract now focuses on one responsibility, making it easier to maintain and extend
}
```
In the improved version, the contract is modularized. The `Deposit` and `Withdraw` contracts are separated into different contracts, each handling one responsibility. The Bank contract then combines these functionalities in a clean and maintainable way.

