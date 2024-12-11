---
title: Circular Dependencies
id: SCWE-004
alias: circular-dependencies
platform: []
profiles: [L1]
mappings:
  scsvs-cg: [SCSVS-ARCH]
  scsvs-scg: [SCSVS-ARCH-2]
  cwe: [835]
status: new
---

## Relationships
- CWE-835: Loop with Unreachable Exit Condition ('Infinite Loop')
  [https://cwe.mitre.org/data/definitions/835.html](https://cwe.mitre.org/data/definitions/835.html)

## Description
Circular dependencies occur when two or more components depend on each other directly or indirectly, creating a loop. In smart contracts, this can lead to issues such as stack overflows, infinite loops, or other unexpected behaviors. Circular dependencies make contracts harder to upgrade, test, and maintain. It can also cause issues during contract initialization, leading to failures when interacting with external systems or other contracts.

## Remediation
- **Refactor Dependencies:** Break the circular dependencies by refactoring the code, ensuring that contracts depend on simpler, independent modules.
- **Use Interfaces:** Instead of direct dependencies, use interfaces to interact with external contracts, which reduces coupling and prevents circular relationships.
- **Separate Responsibilities:** Separate contract logic into distinct modules to avoid interdependencies. Ensure that contracts are focused on one specific responsibility.
- **Upgrade Design:** If upgrading contracts, be mindful of how dependencies between contracts interact. Implement upgradeable proxies to maintain contract state and prevent circular dependency issues.

## Samples

### Example of Circular Dependency:

```solidity
pragma solidity ^0.4.0;

contract ContractA {
    ContractB public contractB;

    function setContractB(address _contractB) public {
        contractB = ContractB(_contractB);
    }

    function callContractB() public {
        contractB.doSomething();
    }
}

contract ContractB {
    ContractA public contractA;

    function setContractA(address _contractA) public {
        contractA = ContractA(_contractA);
    }

    function doSomething() public {
        contractA.callContractB();
    }
}
```
In the above example, `ContractA` and `ContractB` depend on each other, causing a circular dependency.

### Refactored to Avoid Circular Dependency:
```solidity
pragma solidity ^0.4.0;

contract ContractA {
    address public contractB;

    function setContractB(address _contractB) public {
        contractB = _contractB;
    }

    function callContractB() public {
        // Interact with ContractB via an interface
        IContractB(contractB).doSomething();
    }
}

contract ContractB {
    function doSomething() public {
        // Perform logic
    }
}

interface IContractB {
    function doSomething() external;
}
```
In this refactored example, `ContractA` interacts with `ContractB` via an interface, eliminating the circular dependency.
