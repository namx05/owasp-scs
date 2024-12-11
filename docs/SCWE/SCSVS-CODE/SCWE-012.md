---
title: Improper Function Definitions
id: SCWE-012
alias: improper-function-definition
platform: []
profiles: [L1]
mappings:
  scsvs-cg: [SCSVS-CODE]
  scsvs-scg: [SCSVS-CODE-1]
  cwe: [710]
status: new
---

## Relationships
- CWE-710: Improper Adherence to Coding Standards
  [https://cwe.mitre.org/data/definitions/710.html](https://cwe.mitre.org/data/definitions/710.html)

## Description
Improper function definitions refer to situations where functions in smart contracts are defined with incorrect or inconsistent logic, parameter types, or return types. This can lead to unexpected behaviors and vulnerabilities in the contract. Common issues include:

- **Inconsistent parameter types**: Functions that take or return parameters of unexpected or incorrect types.
- **Misleading function names**: Functions with names that do not match their actual behavior.
- **Incorrect visibility**: Functions that are defined with the wrong visibility, either exposing sensitive logic or causing issues with access control.

## Remediation
- **Ensure consistency with function signatures**: Validate that parameters, return types, and function names are correct and consistent with the intended contract logic.
- **Review function visibility**: Double-check that functions are properly marked as `public`, `private`, `internal`, or `external` based on the intended access levels.
- **Follow coding standards**: Adhere to established coding standards for smart contracts to ensure clarity and avoid issues with maintenance or security.

## Samples

### Improper Function Definition

```solidity
pragma solidity ^0.4.0;

contract ImproperFunction {
    uint public balance;

    // Function is defined without specifying return type
    function getBalance() {
        return balance;  // Missing return type (should be 'uint')
    }
}
```

### Correct Function Definition
```solidity
pragma solidity ^0.4.0;

contract CorrectFunction {
    uint public balance;

    // Function correctly defined with return type 'uint'
    function getBalance() public view returns (uint) {
        return balance;
    }
}
```