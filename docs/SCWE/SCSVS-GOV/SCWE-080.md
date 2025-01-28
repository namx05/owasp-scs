---
title: Lack of Circuit Breakers
id: SCWE-080
alias: lack-of-circuit-breakers
platform: []
profiles: [L1]
mappings:
  scsvs-cg: []
  scsvs-scg: []
  cwe: [703]
status: new
---

## Relationships  
- CWE-754: Improper Check for Unusual or Exceptional Conditions  
  [https://cwe.mitre.org/data/definitions/754.html](https://cwe.mitre.org/data/definitions/754.html)  

## Description
A contract that lacks a circuit breaker mechanism can continue operating under unintended or harmful conditions. If a contract encounters a critical error or unexpected situation (such as a vulnerability or an attack), it can be exploited further without a way to halt its operations. Circuit breakers are vital to ensuring that contracts can be paused to prevent further damage.

## Remediation
Implement a circuit breaker that allows for pausing the contract in case of emergencies. The owner or designated address should be able to trigger the pause and resume operations as necessary.

### Vulnerable Contract Example
```solidity
contract Example {
    function execute() public {
        // No way to stop the contract in case of emergency
        // If a bug occurs, the contract is still executing
    }
}
```
### Fixed Contract Example
```solidity
contract Example {
    bool public paused = false;
    address public owner;

    constructor() {
        owner = msg.sender;
    }

    modifier onlyOwner() {
        require(msg.sender == owner, "Not authorized");
        _;
    }

    modifier whenNotPaused() {
        require(!paused, "Contract is paused");
        _;
    }

    function execute() public whenNotPaused {
        // Execute actions
    }

    function togglePause() public onlyOwner {
        paused = !paused;
    }
}
```