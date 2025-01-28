---
title: Insecure Use of msg.sender
id: SCWE-085
alias: insecure-use-of-msg-sender
platform: []
profiles: [L1]
mappings:
  scsvs-cg: []
  scsvs-scg: []
  cwe: [352]
status: new
---

## Relationships  
- CWE-352: Cross-Site Request Forgery (CSRF)  
  [https://cwe.mitre.org/data/definitions/352.html](https://cwe.mitre.org/data/definitions/352.html)  

## Description
Relying solely on `msg.sender` for authorization can be dangerous as it can be spoofed in certain conditions, leading to unauthorized access or actions. If the contract logic does not properly validate `msg.sender`, attackers may be able to trick the contract into performing unauthorized actions.

## Remediation
Ensure proper validation of `msg.sender` and consider using multi-factor authentication or more secure methods for authorization, such as whitelisted addresses or signature verification.

### Vulnerable Contract Example
```solidity
contract Example {
    address public owner;

    constructor() {
        owner = msg.sender;
    }

    function execute() public {
        require(msg.sender == owner, "Unauthorized"); // msg.sender can be spoofed
        // Execute logic
    }
}
```
### Fixed Contract Example
```solidity
contract Example {
    address public owner;

    constructor() {
        owner = msg.sender;
    }

    modifier onlyOwner() {
        require(msg.sender == owner, "Not authorized");
        _;
    }

    function execute() public onlyOwner {
        // Execute logic securely
    }
}
```