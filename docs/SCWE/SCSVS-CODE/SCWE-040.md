---
title: Insecure Use of Block Variables
id: SCWE-040
alias: insecure-use-of-block-variables
platform: []
profiles: [L1]
mappings:
  scsvs-cg: [SCSVS-CODE]
  scsvs-scg: [SCSVS-CODE-2]
  cwe: [20]
status: new
---

## Relationships
- CWE-20: Improper Input Validation  
  [CWE-20 Link](https://cwe.mitre.org/data/definitions/20.html)

## Description  
Insecure use of block variables refers to vulnerabilities that arise when block variables like `block.timestamp` or `block.number` are used improperly. This can lead to:
- Manipulation of contract logic by miners.
- Exploitation of vulnerabilities in time-sensitive operations.
- Loss of funds or data.

## Remediation
- **Avoid reliance on block variables:** Do not use block variables for critical logic.
- **Use secure alternatives:** Leverage external time oracles for accurate time data.
- **Validate inputs:** Ensure all time-based conditions are properly validated.

## Examples
- **Insecure Block Variable Usage**
    ```solidity
    pragma solidity ^0.8.0;

    contract InsecureBlockVariable {
        function isExpired(uint deadline) public view returns (bool) {
            return block.timestamp >= deadline; // Insecure use of block.timestamp
        }
    }
    ```

- **Secure Time Handling**
    ```solidity
    pragma solidity ^0.8.0;

    contract SecureTimeHandling {
        function isExpired(uint deadline, uint currentTime) public pure returns (bool) {
            return currentTime >= deadline; // Secure use of external time data
        }
    }
    ```