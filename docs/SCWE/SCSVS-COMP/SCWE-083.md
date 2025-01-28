---
title: Failure to Handle Edge Cases
id: SCWE-083
alias: failure-to-handle-edge-cases
platform: []
profiles: [L1]
mappings:
  scsvs-cg: [SCSVS-COMP]
  scsvs-scg: [SCSVS-COMP-2]
  cwe: [754]
status: new
---

## Relationships  
- CWE-754: Improper Check for Unusual or Exceptional Conditions  
  [https://cwe.mitre.org/data/definitions/754.html](https://cwe.mitre.org/data/definitions/754.html)  

## Description
Failure to handle edge cases can lead to vulnerabilities in smart contracts. Not accounting for extreme or unexpected conditions can result in bugs, errors, or exploits, which could impact the contract's security or functionality.

## Remediation
Ensure that all edge cases are properly considered and handled during the development of the contract. Utilize `require` and `assert` to ensure proper validation of inputs, outputs, and states.

### Vulnerable Contract Example
```solidity
contract Example {
    function divide(uint256 _numerator, uint256 _denominator) public pure returns (uint256) {
        return _numerator / _denominator; // Division by zero is not checked
    }
}
```
### Fixed Contract Example
```solidity
contract Example {
    function divide(uint256 _numerator, uint256 _denominator) public pure returns (uint256) {
        require(_denominator != 0, "Cannot divide by zero");
        return _numerator / _denominator;
    }
}
```