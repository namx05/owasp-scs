---
title: Lack of Rate Limiting
id: SCWE-077
alias: lack-of-rate-limiting
platform: []
profiles: [L1]
mappings:
  scsvs-cg: []
  scsvs-scg: []
  cwe: [770]
status: new
---

## Relationships  
- CWE-77: Improper Neutralization of Special Elements used in a Command ('Command Injection')  
  [https://cwe.mitre.org/data/definitions/77.html](https://cwe.mitre.org/data/definitions/77.html)  

## Description
The lack of rate limiting in a contract can result in denial of service (DoS) or resource exhaustion. Without mechanisms to limit the number of requests a user can make within a certain time frame, malicious actors can flood the contract with excessive transactions or requests, causing the contract to become unresponsive or unusable.

## Remediation
Implement rate limiting mechanisms using time-based conditions or counters to restrict the number of actions a user can perform in a given period. Ensure that resource consumption is limited to avoid service disruptions.

### Vulnerable Contract Example
```solidity
contract Example {
    mapping(address => uint) public userRequests;

    // No rate limiting, users can make unlimited requests
    function request() public {
        userRequests[msg.sender]++;
    }
}
```
### Fixed Contract Example
```solidity
contract Example {
    mapping(address => uint) public userRequests;
    uint public requestLimit = 5;
    uint public timeWindow = 1 hours;

    // Implement rate limiting
    function request() public {
        require(userRequests[msg.sender] < requestLimit, "Rate limit exceeded");
        userRequests[msg.sender]++;
        // Reset counter after time window
    }
}
```