---
title: Delegatecall to Untrusted Callee
id: SCWE-051
alias: delegatecall-untrusted
platform: []
profiles: [L1]
mappings:
  scsvs-cg: []
  scsvs-scg: []
  cwe: [829]
status: new
---

## Relationships  
- CWE-829: Inclusion of Functionality from Untrusted Control Sphere  
  [https://cwe.mitre.org/data/definitions/829.html](https://cwe.mitre.org/data/definitions/829.html)  

## Description
The `delegatecall` function allows a contract to execute code from another contract while maintaining its own context. Using `delegatecall` to interact with untrusted contracts can lead to critical vulnerabilities, as the callee can manipulate the calling contract's state and potentially execute unauthorized actions.

## Remediation
To mitigate the risks, ensure that `delegatecall` is only used with trusted contracts. Implement access controls and validation mechanisms to prevent malicious contract interactions.

### Vulnerable Contract Example
```solidity
contract Vulnerable {
    address public callee;
    
    function setCallee(address _callee) public {
        callee = _callee;
    }
    
    function callUntrusted(bytes memory data) public {
        (bool success, ) = callee.delegatecall(data);  // Untrusted callee
        require(success, "Call failed");
    }
}
```

### Fixed Contract Example
```solidity
contract Secure {
    address public callee;
    address public owner;
    
    modifier onlyOwner() {
        require(msg.sender == owner, "Not the owner");
        _;
    }

    function setCallee(address _callee) public onlyOwner {
        callee = _callee;
    }

    function callTrusted(bytes memory data) public onlyOwner {
        require(isTrusted(callee), "Untrusted callee");
        (bool success, ) = callee.delegatecall(data);  // Trusted callee
        require(success, "Call failed");
    }
    
    function isTrusted(address _callee) internal view returns (bool) {
        return _callee != address(0);  // Simple check
    }
}
```