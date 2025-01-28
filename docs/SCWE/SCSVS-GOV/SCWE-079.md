---
title: Insecure Use of Transfer and Send
id: SCWE-079
alias: insecure-use-of-transfer-send
platform: []
profiles: [L1]
mappings:
  scsvs-cg: []
  scsvs-scg: []
  cwe: [400]
status: new
---

## Relationships  
- CWE-400: Uncontrolled Resource Consumption  
  [https://cwe.mitre.org/data/definitions/400.html](https://cwe.mitre.org/data/definitions/400.html)  

## Description
Using `transfer()` and `send()` for Ether transfers is insecure because they impose a fixed gas limit (2300 gas). This can lead to failures in cases where the receiving contract requires more gas for execution. Furthermore, the gas limit is insufficient to allow contract logic to execute, potentially resulting in denial of service (DoS).

## Remediation
Use `call()` instead of `transfer()` and `send()` as it provides greater flexibility in handling gas and allows better error checking.

### Vulnerable Contract Example
```solidity
contract Example {
    function transferEther(address payable _to) public payable {
        _to.transfer(msg.value);  // Risk of failure if more gas is required
    }
}
```
### Fixed Contract Example
```solidity
contract Example {
    function transferEther(address payable _to) public payable {
        (bool success, ) = _to.call{value: msg.value}("");  // Use call for flexibility
        require(success, "Transfer failed");
    }
}
```