---
title: Authorization through tx.origin
id: SCWE-066
alias: authorization-through-tx-origin
platform: []
profiles: [L1]
mappings:
  scsvs-cg: []
  scsvs-scg: []
  cwe: [640]
status: new
---

## Relationships  
- CWE-640: Weak Password Recovery Mechanism  
  [https://cwe.mitre.org/data/definitions/640.html](https://cwe.mitre.org/data/definitions/640.html)  

## Description
Using `tx.origin` for authorization in Ethereum smart contracts can introduce significant security risks. `tx.origin` refers to the original address that initiated the transaction, which is not necessarily the caller of the current function. This means that if a contract relies on `tx.origin` for authentication, any external contract can call the vulnerable contract on behalf of the user, bypassing the intended access controls.

Since `tx.origin` can be manipulated by an attacker through a chain of contract calls, it is considered an insecure method for implementing authorization or access control.

## Remediation
To mitigate this vulnerability, avoid using `tx.origin` for authorization or access control. Instead, use `msg.sender`, which represents the immediate caller of the function and is much more reliable for ensuring that only the correct user or contract can execute certain actions.

### Vulnerable Contract Example
```solidity
contract Vulnerable {
    address public owner;

    constructor() {
        owner = msg.sender;
    }

    function sensitiveFunction() public {
        require(tx.origin == owner, "Not authorized");  // Authorization via tx.origin
        // Function logic
    }
}
```

### Fixed Contract Example
```solidity
contract Secure {
    address public owner;

    constructor() {
        owner = msg.sender;
    }

    function sensitiveFunction() public {
        require(msg.sender == owner, "Not authorized");  // Authorization via msg.sender
        // Function logic
    }
}
```