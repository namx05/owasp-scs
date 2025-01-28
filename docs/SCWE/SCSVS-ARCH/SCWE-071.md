---
title: Uninitialized Storage Pointer
id: SCWE-071
alias: uninitialized-storage-pointer
platform: []
profiles: [L1]
mappings:
  scsvs-cg: []
  scsvs-scg: []
  cwe: [457]
status: new
---

## Relationships  
- CWE-457: Use of Uninitialized Variable  
  [https://cwe.mitre.org/data/definitions/457.html](https://cwe.mitre.org/data/definitions/457.html)  

## Description
An uninitialized storage pointer in Solidity refers to a variable that has been declared but not assigned a value before being used. This can result in unpredictable behavior, as the variable might point to unintended locations in the contract's storage, potentially exposing sensitive data or allowing attackers to exploit the uninitialized pointer. This is a critical issue because Solidity does not automatically initialize storage variables, leaving them with default values that may be unsafe.

## Remediation
Always initialize storage pointers to avoid potential vulnerabilities. Ensure that all variables, especially storage pointers, are properly assigned a value before being used. This prevents accessing uninitialized or garbage data from the contract’s storage.

### Vulnerable Contract Example
```solidity
contract Example {
    uint[] public data;

    // Uninitialized storage pointer, could lead to unexpected behavior
    function addData(uint _value) public {
        data.push(_value);
        uint[] storage uninitializedPointer;  // Pointer is uninitialized
        uninitializedPointer.push(10);  // Accessing uninitialized storage pointer
    }
}
```

### Fixed Contract Example
```solidity
contract Example {
    uint[] public data;

    function addData(uint _value) public {
        data.push(_value);
        uint[] storage initializedPointer = data;  // Properly initialized storage pointer
        initializedPointer.push(10);  // Now safely interacting with the initialized pointer
    }
}
```